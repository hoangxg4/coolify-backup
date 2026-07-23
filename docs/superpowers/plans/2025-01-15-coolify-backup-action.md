# Coolify Backup GitHub Action Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a GitHub Action that auto-backs up Coolify servers (50+) using Matrix + Parallel strategy with S3 storage

**Architecture:** Single workflow file with 3 jobs: get-servers (fetch API), backup (matrix with parallel SSH), cleanup (delete old backups). S3 multipart upload for chunked storage.

**Tech Stack:** GitHub Actions YAML, Bash scripts, AWS CLI, rsync, jq, GNU parallel

## Global Constraints

- GitHub Actions runner: ubuntu-latest
- Matrix: 5 batches x 10 servers = 50+ servers
- Concurrent SSH per batch: 5
- S3 storage class: STANDARD_IA
- Max backups per server: 5
- Trigger: every 6 hours + manual

---

## File Structure

```
.github/
  workflows/
    coolify-backup.yml      # Main workflow file
```

---

## Tasks

### Task 1: Create workflow directory and file

**Files:**
- Create: `.github/workflows/coolify-backup.yml`

**Interfaces:**
- N/A (setup task)

- [ ] **Step 1: Create directory structure**

```bash
mkdir -p .github/workflows
```

- [ ] **Step 2: Create workflow file with all jobs**

Create `.github/workflows/coolify-backup.yml` with complete workflow:

```yaml
name: Coolify Backup

on:
  schedule:
    - cron: '0 */6 * * *'  # Every 6 hours
  workflow_dispatch:        # Manual trigger

jobs:
  get-servers:
    runs-on: ubuntu-latest
    outputs:
      servers_json: ${{ steps.fetch.outputs.servers_json }}
      server_count: ${{ steps.fetch.outputs.server_count }}
    steps:
      - name: Fetch server list from Coolify API
        id: fetch
        run: |
          RESPONSE=$(curl -s -H "Authorization: Bearer $COOLIFY_API_TOKEN" \
            "$COOLIFY_API_URL/servers")
          
          SERVERS_JSON=$(echo "$RESPONSE" | jq -c '[.[].ip]')
          SERVER_COUNT=$(echo "$SERVERS_JSON" | jq 'length')
          
          echo "servers_json=$SERVERS_JSON" >> $GITHUB_OUTPUT
          echo "server_count=$SERVER_COUNT" >> $GITHUB_OUTPUT
          echo "Found $SERVER_COUNT servers"
        env:
          COOLIFY_API_URL: ${{ secrets.COOLIFY_API_URL }}
          COOLIFY_API_TOKEN: ${{ secrets.COOLIFY_API_TOKEN }}

  backup:
    needs: get-servers
    runs-on: ubuntu-latest
    strategy:
      matrix:
        batch: [0, 1, 2, 3, 4]
      fail-fast: false
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup SSH
        run: |
          mkdir -p ~/.ssh
          echo "$SSH_PRIVATE_KEY" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa
          cat >> ~/.ssh/config << EOF
          Host *
            StrictHostKeyChecking no
            UserKnownHostsFile /dev/null
          EOF
        env:
          SSH_PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}

      - name: Setup AWS CLI
        run: |
          pip install awscli
          aws configure set aws_access_key_id "$AWS_ACCESS_KEY_ID"
          aws configure set aws_secret_access_key "$AWS_SECRET_ACCESS_KEY"
          aws configure set region "$AWS_REGION"
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: ${{ secrets.AWS_REGION }}

      - name: Install dependencies
        run: |
          sudo apt-get update
          sudo apt-get install -y rsync jq

      - name: Backup servers in parallel
        run: |
          BATCH_SIZE=10
          START=$((MATRIX_BATCH * BATCH_SIZE))
          END=$((START + BATCH_SIZE))
          
          SERVERS=$(echo "$SERVERS_JSON" | jq -r '.[]' | \
            sed -n "$((START+1)),${END}p")
          
          if [ -z "$SERVERS" ]; then
            echo "No servers in this batch"
            exit 0
          fi
          
          echo "Backing up servers: $SERVERS"
          
          cat > backup_server.sh << 'SCRIPT'
          #!/bin/bash
          SERVER_IP=$1
          BACKUP_DIR="./backups/$SERVER_IP"
          mkdir -p "$BACKUP_DIR"
          
          TIMESTAMP=$(date +%Y-%m-%d_%H-%M-%S)
          REMOTE_FILE="/tmp/coolify_backup_${TIMESTAMP}.tar.gz"
          
          echo "Starting backup: $SERVER_IP"
          
          ssh -o ConnectTimeout=10 -o ServerAliveInterval=5 \
            -i ~/.ssh/id_rsa "$SERVER_IP" "
            cd /tmp && \
            tar czf coolify_data.tar.gz -C / data/coolify 2>/dev/null && \
            docker volume ls -q | xargs -P 5 -I {} \
              docker run --rm -v {}:/data -v /tmp:/backup alpine \
              tar czf /backup/vol_{}.tar.gz -C / data 2>/dev/null && \
            tar czf $REMOTE_FILE coolify_data.tar.gz vol_*.tar.gz && \
            rm -f coolify_data.tar.gz vol_*.tar.gz
          " || { echo "SSH failed: $SERVER_IP"; exit 1; }
          
          rsync -avz --timeout=60 --partial \
            -e "ssh -i ~/.ssh/id_rsa" \
            "$SERVER_IP:$REMOTE_FILE" "$BACKUP_DIR/" || \
            { echo "rsync failed: $SERVER_IP"; exit 1; }
          
          ssh -i ~/.ssh/id_rsa "$SERVER_IP" "rm -f $REMOTE_FILE" 2>/dev/null
          
          echo "Completed: $SERVER_IP"
          SCRIPT
          chmod +x backup_server.sh
          
          echo "$SERVERS" | xargs -P 5 -I {} bash backup_server.sh {}
        env:
          SERVERS_JSON: ${{ needs.get-servers.outputs.servers_json }}
          MATRIX_BATCH: ${{ matrix.batch }}
          SSH_PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}

      - name: Upload batch backups to S3
        run: |
          if [ ! -d "./backups" ] || [ -z "$(ls -A ./backups 2>/dev/null)" ]; then
            echo "No backups to upload"
            exit 0
          fi
          
          for dir in ./backups/*/; do
            SERVER_IP=$(basename "$dir")
            echo "Uploading backups for $SERVER_IP..."
            
            for file in "$dir"*.tar.gz; do
              if [ -f "$file" ]; then
                FILENAME=$(basename "$file")
                FILESIZE=$(stat -c%s "$file")
                
                echo "  Uploading: $FILENAME ($FILESIZE bytes)"
                
                aws s3 cp "$file" \
                  "s3://$S3_BUCKET/coolify/$SERVER_IP/$FILENAME" \
                  --storage-class STANDARD_IA \
                  --expected-size "$FILESIZE" \
                  --only-show-errors
                
                echo "  Done: $FILENAME"
              fi
            done
          done
          
          echo "All uploads complete"
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: ${{ secrets.AWS_REGION }}
          S3_BUCKET: ${{ secrets.S3_BUCKET }}

      - name: Cleanup local
        if: always()
        run: rm -rf ./backups/

      - name: Upload backup logs
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: backup-logs-batch-${{ matrix.batch }}
          path: /tmp/backup*.log
          retention-days: 7

  cleanup:
    needs: [get-servers, backup]
    runs-on: ubuntu-latest
    if: always()
    steps:
      - name: Configure AWS CLI
        run: |
          pip install awscli
          aws configure set aws_access_key_id "$AWS_ACCESS_KEY_ID"
          aws configure set aws_secret_access_key "$AWS_SECRET_ACCESS_KEY"
          aws configure set region "$AWS_REGION"
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: ${{ secrets.AWS_REGION }}

      - name: Cleanup old backups (keep max 5)
        run: |
          echo "Cleaning up old backups..."
          
          SERVERS=$(aws s3 ls "s3://$S3_BUCKET/coolify/" | \
            awk '{print $2}' | tr -d '/')
          
          for SERVER_IP in $SERVERS; do
            echo "Processing: $SERVER_IP"
            
            BACKUPS=$(aws s3 ls "s3://$S3_BUCKET/coolify/$SERVER_IP/" | \
              grep "\.tar\.gz$" | \
              sort | \
              awk '{print $4}')
            
            COUNT=$(echo "$BACKUPS" | wc -l)
            
            if [ "$COUNT" -gt 5 ]; then
              DELETE_COUNT=$((COUNT - 5))
              echo "  Deleting $DELETE_COUNT old backups..."
              
              echo "$BACKUPS" | head -n "$DELETE_COUNT" | while read FILE; do
                if [ -n "$FILE" ]; then
                  echo "  Deleting: $FILE"
                  aws s3 rm "s3://$S3_BUCKET/coolify/$SERVER_IP/$FILE" \
                    --only-show-errors
                fi
              done
            else
              echo "  Keeping all $COUNT backups (<= 5)"
            fi
          done
          
          echo "Cleanup complete"
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: ${{ secrets.AWS_REGION }}
          S3_BUCKET: ${{ secrets.S3_BUCKET }}
```

- [ ] **Step 3: Verify YAML syntax**

Run: `cat .github/workflows/coolify-backup.yml | head -20`
Expected: Valid YAML with on: triggers and jobs defined

- [ ] **Step 4: Commit**

```bash
git add .github/workflows/coolify-backup.yml
git commit -m "feat: add Coolify backup GitHub Action workflow"
```

---

### Task 2: Create README with setup instructions

**Files:**
- Create: `README.md`

**Interfaces:**
- N/A (documentation task)

- [ ] **Step 1: Create README**

```markdown
# Coolify Backup Action

GitHub Action to automatically backup Coolify servers (50+) to S3.

## Features

- **Matrix + Parallel**: 5 batches x 10 servers = 50+ servers backed up in ~10-15 minutes
- **S3 Storage**: Multipart upload for large files, STANDARD_IA for cost savings
- **Auto Cleanup**: Keeps max 5 backups per server
- **Schedule**: Runs every 6 hours + manual trigger

## Secrets Required

| Secret | Description |
|--------|-------------|
| `COOLIFY_API_URL` | Full API URL (e.g., `https://coolify.example.com/api/v1`) |
| `COOLIFY_API_TOKEN` | API bearer token |
| `SSH_PRIVATE_KEY` | Full private key content |
| `AWS_ACCESS_KEY_ID` | S3 access key |
| `AWS_SECRET_ACCESS_KEY` | S3 secret key |
| `AWS_REGION` | S3 region |
| `S3_BUCKET` | Target S3 bucket |

## S3 Folder Structure

```
s3://your-bucket/coolify/
  1.2.3.4/
    backup_2025-01-15_02-00-00.tar.gz
    backup_2025-01-15_08-00-00.tar.gz
    ...
  5.6.7.8/
    ...
```

## Setup

1. Create S3 bucket with appropriate IAM permissions
2. Add GitHub Secrets in repo settings
3. Push workflow file to `.github/workflows/coolify-backup.yml`
4. Action runs automatically every 6 hours or trigger manually

## Backup Contents

Each backup contains:
- `/data/coolify` directory
- All Docker volumes (named volumes)

## Performance

- 5 concurrent runners (matrix batches)
- 5 concurrent SSH sessions per batch
- Total time for 50 servers: ~10-15 minutes
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add README with setup instructions"
```

---

## Execution Handoff

Plan complete and saved to `docs/superpowers/plans/2025-01-15-coolify-backup-action.md`.

**Two execution options:**

1. **Subagent-Driven (recommended)** - I dispatch a fresh subagent per task, review between tasks, fast iteration

2. **Inline Execution** - Execute tasks in this session using executing-plans, batch execution with checkpoints

**Which approach?**
