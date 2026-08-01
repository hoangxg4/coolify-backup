# Coolify Backup Action

GitHub Action tự động backup các Coolify servers (50+) lên rclone remote storage.

## Tính năng

- **Matrix + Parallel**: 5 batches x 10 servers = 50+ servers backup trong ~10-15 phút
- **rclone Storage**: Parallel chunked upload tới bất kỳ remote nào (S3, B2, Drive, v.v.)
- **Auto Cleanup**: Giữ tối đa 5 bản backup/server
- **Schedule**: Chạy mỗi 6 tiếng + manual trigger

## Secrets cần setup

| Secret | Mô tả | Ví dụ |
|--------|-------|-------|
| `COOLIFY_API_URL` | Full API URL | `https://coolify.example.com/api/v1` |
| `COOLIFY_API_TOKEN` | API bearer token | `xxxxxxxxxxxx` |
| `SSH_PRIVATE_KEY` | Full private key content | `-----BEGIN OPENSSH PRIVATE KEY-----...` |
| `RCLONE_CONFIG` | Full rclone config file content | `[myremote]\ntype = s3\nprovider = ...` |
| `RCLONE_REMOTE` | Remote name + base path | `myremote:coolify-backups` |

## Remote Folder Structure

```
<rclone_remote>/
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

## Setup

1. Tạo rclone remote local:
   ```bash
   rclone config
   # Tạo remote (vd: "myremote") với storage provider của bạn
   ```

2. Copy nội dung `~/.config/rclone/rclone.conf` vào Secret `RCLONE_CONFIG`

3. Thêm các GitHub Secrets khác trong repo settings:
   - `COOLIFY_API_URL`, `COOLIFY_API_TOKEN`
   - `SSH_PRIVATE_KEY`
   - `RCLONE_CONFIG`, `RCLONE_REMOTE`

4. Push workflow file `.github/workflows/coolify-backup.yml`

5. Action tự chạy mỗi 6 tiếng hoặc trigger manual

## Backup Contents

Mỗi backup gồm:
- `/data/coolify` directory
- Tất cả Docker volumes (named volumes)

## Performance

- 5 concurrent runners (matrix batches)
- 5 concurrent SSH sessions per batch
- Tổng thời gian cho 50 servers: ~10-15 phút

## Tạo rclone remote

Ví dụ tạo remote S3-compatible:

```bash
rclone config
# n) New remote
# name> myremote
# Storage > s3
# provider > Other
# endpoint > https://s3.example.com
# access_key_id > ...
# secret_access_key > ...
# region > us-east-1
```

Sau đó copy config:
```bash
cat ~/.config/rclone/rclone.conf
# Paste nội dung vào Secret RCLONE_CONFIG
```
