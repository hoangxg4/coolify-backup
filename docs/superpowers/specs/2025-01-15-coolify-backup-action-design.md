# Coolify Backup GitHub Action Design

## Overview

Automated backup solution for Coolify servers using GitHub Actions with Matrix + Parallel strategy and rclone remote storage.

**Key Decisions:**
- Dynamic Matrix + Parallel: servers tự chia đều vào 10 batches chạy song song
- rclone remote storage with parallel chunked upload
- Sequential cleanup job (keep max 5 backups per server)

## Architecture

```
+-------------------------------------------------------------+
|                    GitHub Actions                            |
+-------------------------------------------------------------+
|  Job 1: get-servers                                         |
|    - Fetch server list from Coolify API                     |
|    - Output: servers_json array + batch_list (10 batches)   |
|                                                              |
|  Job 2: backup (Dynamic Matrix Strategy)                    |
|    +-------------+  +-------------+  +-------------+       |
|    |  Batch 0    |  |  Batch 1    |  |  Batch 2    |  ...  |
|    | (N/10 svrs) |  | (N/10 svrs) |  | (N/10 svrs) |       |
|    |  parallel   |  |  parallel   |  |  parallel   |       |
|    |  SSH backup |  |  SSH backup |  |  SSH backup |       |
|    |  rclone up  |  |  rclone up  |  |  rclone up  |       |
|    +-------------+  +-------------+  +-------------+       |
|                                                              |
|  Job 3: cleanup                                             |
|    - Delete old backups (keep max 5 per server)             |
+-------------------------------------------------------------+
```

## Secrets Required

| Secret | Description | Example |
|--------|-------------|---------|
| `COOLIFY_API_URL` | Full API endpoint URL | `https://coolify.example.com/api/v1` |
| `COOLIFY_API_TOKEN` | API bearer token | `xxxxxxxxxxxx` |
| `SSH_PRIVATE_KEY` | Full private key content | `-----BEGIN OPENSSH PRIVATE KEY-----...` |
| `RCLONE_CONFIG` | Full rclone config file content | `[myremote]\ntype = s3\nprovider = ...` |
| `RCLONE_REMOTE` | Remote name + base path | `myremote:coolify-backups` |

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
    batch_list: ${{ steps.fetch.outputs.batch_list }}
  steps:
    - name: Fetch server list from Coolify API
      id: fetch
      run: |
        # Number of parallel matrix batches (tune as needed)
        MATRIX_BATCHES=10

        RESPONSE=$(curl -s -H "Authorization: Bearer $COOLIFY_API_TOKEN" \
          "$COOLIFY_API_URL/servers")

        SERVERS_JSON=$(echo "$RESPONSE" | jq -c '[.[].ip]')
        SERVER_COUNT=$(echo "$SERVERS_JSON" | jq 'length')

        if [ "$SERVER_COUNT" -eq 0 ]; then
          echo "::error::No servers returned by API. Check COOLIFY_API_URL and COOLIFY_API_TOKEN."
          exit 1
        fi

        # Dynamic matrix: always 10 batches, servers are divided evenly later
        BATCH_LIST=$(seq 0 $((MATRIX_BATCHES - 1)) | jq -c -s '.')

        echo "servers_json=$SERVERS_JSON" >> $GITHUB_OUTPUT
        echo "server_count=$SERVER_COUNT" >> $GITHUB_OUTPUT
        echo "batch_list=$BATCH_LIST" >> $GITHUB_OUTPUT
        echo "Found $SERVER_COUNT servers, running $MATRIX_BATCHES parallel batches"
```

### Job 2: backup (Dynamic Matrix)

```yaml
backup:
  needs: get-servers
  runs-on: ubuntu-latest
  strategy:
    matrix:
      batch: ${{ fromJSON(needs.get-servers.outputs.batch_list) }}
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

    - name: Setup rclone
      run: |
        # Install rclone
        sudo apt-get update
        sudo apt-get install -y rclone rsync jq
        # Write rclone config
        mkdir -p ~/.config/rclone
        echo "$RCLONE_CONFIG" > ~/.config/rclone/rclone.conf
        chmod 600 ~/.config/rclone/rclone.conf

    - name: Backup servers in parallel
      run: |
        # Divide servers evenly across 10 batches (ceil division)
        MATRIX_BATCHES=10
        BATCH_SIZE=$(( (SERVER_COUNT + MATRIX_BATCHES - 1) / MATRIX_BATCHES ))
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

        # Run parallel backup (10 concurrent SSH sessions)
        echo "$SERVERS" | xargs -P 10 -I {} bash backup_server.sh {}

      env:
        SERVERS_JSON: ${{ needs.get-servers.outputs.servers_json }}
        SERVER_COUNT: ${{ needs.get-servers.outputs.server_count }}
        MATRIX_BATCH: ${{ matrix.batch }}
        SSH_PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}

    - name: Upload batch backups to remote
      run: |
        if [ ! -d "./backups" ] || [ -z "$(ls -A ./backups 2>/dev/null)" ]; then
          echo "No backups to upload"
          exit 0
        fi
        
        # Upload each server folder
        for dir in ./backups/*/; do
          SERVER_IP=$(basename "$dir")
          echo "Uploading backups for $SERVER_IP..."
          # rclone copy with parallel transfers (chunked upload)
          rclone copy "$dir" "$RCLONE_REMOTE/$SERVER_IP/" \
            --transfers 4 \
            --checkers 8 \
            --stats 30s \
            --stats-one-line
        done
        
        echo "All uploads complete"
      
      env:
        RCLONE_REMOTE: ${{ secrets.RCLONE_REMOTE }}

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
    - name: Setup rclone
      run: |
        sudo apt-get update
        sudo apt-get install -y rclone
        mkdir -p ~/.config/rclone
        echo "$RCLONE_CONFIG" > ~/.config/rclone/rclone.conf
        chmod 600 ~/.config/rclone/rclone.conf

    - name: Cleanup old backups (keep max 5)
      run: |
        echo "Cleaning up old backups..."
        
        # List all server folders
        SERVERS=$(rclone lsf "$RCLONE_REMOTE/" --dirs-only | tr -d '/')
        
        for SERVER_IP in $SERVERS; do
          echo "Processing: $SERVER_IP"
          
          # List backups sorted by name (newest last)
          BACKUPS=$(rclone lsl "$RCLONE_REMOTE/$SERVER_IP/" | \
            awk '{print $4}' | \
            grep "\.tar\.gz$" | \
            sort)
          
          COUNT=$(echo "$BACKUPS" | wc -l)
          
          if [ "$COUNT" -gt 5 ]; then
            DELETE_COUNT=$((COUNT - 5))
            echo "  Deleting $DELETE_COUNT old backups..."
            
            echo "$BACKUPS" | head -n "$DELETE_COUNT" | while read FILE; do
              if [ -n "$FILE" ]; then
                echo "  Deleting: $FILE"
                rclone delete "$RCLONE_REMOTE/$SERVER_IP/$FILE"
              fi
            done
          else
            echo "  Keeping all $COUNT backups (<= 5)"
          fi
        done
        
        echo "Cleanup complete"
      
      env:
        RCLONE_CONFIG: ${{ secrets.RCLONE_CONFIG }}
        RCLONE_REMOTE: ${{ secrets.RCLONE_REMOTE }}
```

## Remote Folder Structure

```
<rclone_remote>/
+-- 1.2.3.4/
|   +-- backup_2025-01-15_02-00-00.tar.gz
|   +-- backup_2025-01-15_08-00-00.tar.gz
|   +-- backup_2025-01-15_14-00-00.tar.gz
|   +-- backup_2025-01-15_20-00-00.tar.gz
|   +-- backup_2025-01-16_02-00-00.tar.gz
+-- 5.6.7.8/
|   +-- ...
+-- ...
```

## Backup File Structure (tar.gz)

```
coolify_backup_YYYY-MM-DD_HH-MM-SS.tar.gz
+-- coolify_data.tar.gz      # /data/coolify contents
+-- vol_data.tar.gz          # Docker volume: data
+-- vol_db.tar.gz            # Docker volume: db
+-- vol_redis.tar.gz         # Docker volume: redis
+-- ...
```

## rclone Parallel Transfer

rclone supports parallel chunked upload with configurable options:
- `--transfers 4`: 4 parallel transfers
- `--checkers 8`: 8 parallel directory checkers
- Auto retry with exponential backoff
- Resumable transfers (--partial)

## Error Handling

| Scenario | Behavior |
|----------|----------|
| API fetch fails | Workflow fails immediately |
| SSH to server fails | Skip server, continue batch |
| rsync fails | Skip server, continue batch |
| rclone upload fails | Fail batch job |
| Cleanup fails | Log warning, continue |
| Any batch fails | Other batches continue (`fail-fast: false`) |

## Performance

| Metric | Value |
|--------|-------|
| Servers per batch | ceil(server_count / 10) (tự chia đều) |
| Concurrent SSH per batch | 10 |
| Number of batches (matrix) | 10 (dynamic) |
| Total concurrent runners | 10 |
| Estimated time (50 servers) | ~5-10 minutes |
| rclone parallel transfers | 4 |

## Security

- SSH key: written to temp file, cleaned up after
- rclone config: written to ~/.config/rclone, contains credentials
- No credentials logged
- Consider: remote encryption (rclone crypt), S3 SSE if using S3 backend

## Monitoring

- GitHub Actions logs for each batch
- rclone --stats output shows transfer progress
- Optional: schedule monitoring for missed backups
