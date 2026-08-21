# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #100 (id `32456545204`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-08-21T06:57:45Z |
| **Duration** | 26m 04s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 76 (in 10 batch(es))
- **Backup OK**: 58
- **Failed**: 18
- **Partial (data/coolify missing, volumes only)**: 0
- **Upload failed**: 13
- **Cleanup**: 79 server dir(s) scanned, 46 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 173.249.50.12 | backup failed (ssh rc=255) |
| 202.182.120.138 | backup failed (ssh rc=255) |
| 75.119.149.222 | backup failed (ssh rc=124) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 45.77.45.79 | backup failed (ssh rc=255) |
| 8.138.177.38 | backup failed (ssh rc=2) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 149.28.156.246 | backup failed (ssh rc=255) |
| 95.217.114.51 | backup failed (ssh rc=255) |
| 46.225.163.149 | backup failed (ssh rc=255) |
| 5.129.206.12 | backup failed (ssh rc=124) |
| 203.175.10.199 | backup failed (ssh rc=255) |
| 82.165.41.87 | backup failed (ssh rc=255) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 173.212.234.212 | backup failed (ssh rc=124) |
| 5.189.191.35 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 209.126.13.81 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| - | None |

## Upload failures

| Host | Reason |
|---|---|
| 107.175.127.199 | rclone copy failed |
| 103.6.169.194 | rclone copy failed |
| 158.247.195.77 | rclone copy failed |
| 188.245.32.1 | rclone copy failed |
| 155.138.175.104 | rclone copy failed |
| 176.9.89.217 | rclone copy failed |
| 185.222.242.202 | rclone copy failed |
| 167.233.120.15 | rclone copy failed |
| 84.247.168.168 | rclone copy failed |
| 217.154.254.251 | rclone copy failed |
| 35.237.115.96 | rclone copy failed |
| 62.238.41.18 | rclone copy failed |
| 140.82.30.182 | rclone copy failed |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 8 | 7 | 1 |
| 1 | 8 | 6 | 2 |
| 2 | 8 | 6 | 2 |
| 3 | 8 | 5 | 3 |
| 4 | 8 | 5 | 3 |
| 5 | 8 | 8 | 0 |
| 6 | 8 | 4 | 4 |
| 7 | 8 | 5 | 3 |
| 8 | 8 | 8 | 0 |
| 9 | 4 | 4 | 0 |
