# Coolify Backup GitHub Action Design

## Overview

Automated backup solution for Coolify servers using GitHub Actions with Matrix + Parallel strategy and S3 storage.

**Key Decisions:**
- Matrix + Parallel: 5 batches × 10 servers = 50+ servers
- S3 storage with multipart upload (chunked)
- Sequential cleanup job

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    GitHub Actions                            │
├─────────────────────────────────────────────────────────────┤
│  Job 1: get-servers                                         │
│    - Fetch server list from Coolify API                     │
│    - Output: servers_json array                             │
│                                                              │
│  Job 2: backup (Matrix Strategy)                            │
│    ┌─────────────┐  ┌─────────────┐  ┌─────────────┐       │
│    │  Batch 0    │  │  Batch 1    │  │  Batch 2    │  ...  │
│    │ (10 servers)│  │ (10 servers)│  │ (10 servers)│       │
│    │  parallel   │  │  parallel   │  │  parallel   │       │
│    │  SSH backup │  │  SSH backup │  │  SSH backup │       │
│    │  S3 upload  │  │  S3 upload  │  │  S3 upload  │       │
│    └─────────────┘  └─────────────┘  └─────────────┘       │
│                                                              │
│  Job 3: cleanup                                             │
│    - Delete old backups (keep max 5 per server)             │
└─────────────────────────────────────────────────────────────┘
```

## Secrets Required

| Secret | Description | Example |
|--------|-------------|---------|
| `COOLIFY_API_URL` | Full API endpoint URL | `https://coolify.example.com/api/v1` |
| `COOLIFY_API_TOKEN` | API bearer token | `xxxxxxxxxxxx` |
| `SSH_PRIVATE_KEY` | Full private key content | `-----BEGIN OPENSSH PRIVATE KEY-----...` |
| `AWS_ACCESS_KEY_ID` | S3 access key | `AKIAIOSFODNN7EXAMPLE` |
| `AWS_SECRET_ACCESS_KEY` | S3 secret key | `wJalrXUtnFEMI/K7MDENG...` |
| `AWS_REGION` | S3 bucket region | `us-east-1` |
| `S3_BUCKET` | Target S3 bucket | `my-coolify-backups` |

## Workflow: coolify-backup.yml

### Trigger

```yaml
on:
  schedule:
    - cron: '0 */6 * * *'  # Every 6 hours
  workflow_dispatch:        # Manual trigger
```

### Job 1: get-servers

```yaml
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
```

### Job 2: backup (Matrix)

```yaml
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
        # Disable strict host checking for automation
        cat >> ~/.ssh/config << EOF
        Host *
          StrictHostKeyChecking no
          UserKnownHostsFile /dev/null
        EOF

    - name: Setup AWS CLI
      run: |
        pip install awscli
        aws configure set aws_access_key_id "$AWS_ACCESS_KEY_ID"
        aws configure set aws_secret_access_key "$AWS_SECRET_ACCESS_KEY"
        aws configure set region "$AWS_REGION"

    - name: Install dependencies
      run: |
        sudo apt-get update
        sudo apt-get install -y rsync jq

    - name: Backup servers in parallel
      run: |
        # Calculate batch range
        BATCH_SIZE=10
        START=$((MATRIX_BATCH * BATCH_SIZE))
        END=$((START + BATCH_SIZE))
        
        # Get servers for this batch
        SERVERS=$(echo "$SERVERS_JSON" | jq -r '.[]' | \
          sed -n "$((START+1)),${END}p")
        
        if [ -z "$SERVERS" ]; then
          echo "No servers in this batch"
          exit 0
        fi
        
        echo "Backing up servers: $SERVERS"
        
        # Create backup script
        cat > backup_server.sh << 'SCRIPT'
        #!/bin/bash
        SERVER_IP=$1
        BACKUP_DIR="./backups/$SERVER_IP"
        mkdir -p "$BACKUP_DIR"
        
        TIMESTAMP=$(date +%Y-%m-%d_%H-%M-%S)
        REMOTE_FILE="/tmp/coolify_backup_${TIMESTAMP}.tar.gz"
        
        echo "Starting backup: $SERVER_IP"
        
        # SSH + tar on server
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
        
        # rsync download
        rsync -avz --timeout=60 --partial \
          -e "ssh -i ~/.ssh/id_rsa" \
          "$SERVER_IP:$REMOTE_FILE" "$BACKUP_DIR/" || \
          { echo "rsync failed: $SERVER_IP"; exit 1; }
        
        # Cleanup remote
        ssh -i ~/.ssh/id_rsa "$SERVER_IP" "rm -f $REMOTE_FILE" 2>/dev/null
        
        echo "Completed: $SERVER_IP"
        SCRIPT
        chmod +x backup_server.sh
        
        # Run parallel backup (5 concurrent SSH sessions)
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
              
              # AWS CLI automatically uses multipart for files > 8MB
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
```

### Job 3: cleanup

```yaml
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

    - name: Cleanup old backups (keep max 5)
      run: |
        echo "Cleaning up old backups..."
        
        # List all server folders
        SERVERS=$(aws s3 ls "s3://$S3_BUCKET/coolify/" | \
          awk '{print $2}' | tr -d '/')
        
        for SERVER_IP in $SERVERS; do
          echo "Processing: $SERVER_IP"
          
          # Get all backups sorted by name (newest last)
          BACKUPS=$(aws s3 ls "s3://$S3_BUCKET/coolify/$SERVER_IP/" | \
            grep "\.tar\.gz$" | \
            sort | \
            awk '{print $4}')
          
          COUNT=$(echo "$BACKUPS" | wc -l)
          
          if [ "$COUNT" -gt 5 ]; then
            # Delete oldest backups (all but last 5)
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

## S3 Folder Structure

```
s3://your-bucket/coolify/
├── 1.2.3.4/
│   ├── backup_2025-01-15_02-00-00.tar.gz
│   ├── backup_2025-01-15_08-00-00.tar.gz
│   ├── backup_2025-01-15_14-00-00.tar.gz
│   ├── backup_2025-01-15_20-00-00.tar.gz
│   └── backup_2025-01-16_02-00-00.tar.gz
├── 5.6.7.8/
│   └── ...
└── ...
```

## Backup File Structure (tar.gz)

```
coolify_backup_YYYY-MM-DD_HH-MM-SS.tar.gz
├── coolify_data.tar.gz      # /data/coolify contents
├── vol_data.tar.gz          # Docker volume: data
├── vol_db.tar.gz            # Docker volume: db
├── vol_redis.tar.gz         # Docker volume: redis
└── ...
```

## S3 Multipart Upload

AWS CLI automatically uses multipart upload for files > 8MB:
- Part size: 100MB (default)
- Concurrent parts: 10
- Retry: automatic with exponential backoff

For manual control:
```bash
aws s3 cp large-file.tar.gz s3://bucket/path/ \
  --storage-class STANDARD_IA \
  --expected-size $(stat -c%s large-file.tar.gz) \
  --part-size 100MB \
  --cli-read-timeout 0 \
  --cli-connect-timeout 60
```

## Error Handling

| Scenario | Behavior |
|----------|----------|
| API fetch fails | Workflow fails immediately |
| SSH to server fails | Skip server, continue batch |
| rsync fails | Skip server, continue batch |
| S3 upload fails | Fail batch job |
| Cleanup fails | Log warning, continue |
| Any batch fails | Other batches continue (`fail-fast: false`) |

## Performance

| Metric | Value |
|--------|-------|
| Servers per batch | 10 |
| Concurrent SSH per batch | 5 |
| Number of batches (matrix) | 5 |
| Total concurrent runners | 5 |
| Estimated time (50 servers) | ~10-15 minutes |
| S3 storage class | STANDARD_IA |

## Security

- SSH key: written to temp file, cleaned up after
- AWS credentials: passed via environment variables
- No credentials logged (use `--only-show-errors`)
- S3 bucket should have proper IAM policies
- Consider: encryption at rest (S3 SSE), encryption in transit (SSL)

## Monitoring

- GitHub Actions logs for each batch
- S3 versioning recommended for backup safety
- Optional: CloudWatch metrics for backup sizes
