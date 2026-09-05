# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #154 (id `33960581670`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-09-05T10:24:40Z |
| **Duration** | 14m 52s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 90 (in 10 batch(es))
- **Backup OK**: 59
- **Failed**: 31
- **Partial (data/coolify missing, volumes only)**: 0
- **Upload failed**: 1
- **Cleanup**: 90 server dir(s) scanned, 58 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 107.175.31.141 | backup failed (ssh rc=255) |
| 173.249.50.12 | backup failed (ssh rc=255) |
| 65.108.63.189 | backup failed (ssh rc=255) |
| 35.254.77.18 | backup failed (ssh rc=255) |
| 157.90.10.4 | backup failed (ssh rc=255) |
| 66.63.168.31 | backup failed (ssh rc=255) |
| 202.182.120.138 | backup failed (ssh rc=255) |
| 8.138.177.38 | backup failed (ssh rc=255) |
| 124.174.76.213 | backup failed (ssh rc=2) |
| 46.225.163.149 | backup failed (ssh rc=255) |
| 43.139.230.5 | backup failed (ssh rc=255) |
| 95.217.114.51 | backup failed (ssh rc=255) |
| 5.189.191.35 | backup failed (ssh rc=255) |
| 43.153.151.229 | backup failed (ssh rc=255) |
| 82.165.41.87 | backup failed (ssh rc=255) |
| 5.161.237.225 | backup failed (ssh rc=255) |
| 141.136.44.86 | backup failed (ssh rc=255) |
| 173.212.234.212 | backup failed (ssh rc=124) |
| 35.222.248.189 | backup failed (ssh rc=255) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 45.77.45.79 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 209.126.13.81 | backup failed (ssh rc=255) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 75.119.149.222 | backup failed (ssh rc=124) |
| 151.242.2.207 | backup failed (ssh rc=255) |
| 124.222.18.52 | backup failed (ssh rc=255) |
| 149.28.156.246 | backup failed (ssh rc=255) |
| 62.113.101.80 | backup failed (ssh rc=255) |
| 5.129.206.12 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| - | None |

## Upload failures

| Host | Reason |
|---|---|
| 62.238.41.18 | rclone copy failed |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 9 | 5 | 4 |
| 1 | 9 | 8 | 1 |
| 2 | 9 | 7 | 2 |
| 3 | 9 | 7 | 2 |
| 4 | 9 | 6 | 3 |
| 5 | 9 | 3 | 6 |
| 6 | 9 | 5 | 4 |
| 7 | 9 | 5 | 4 |
| 8 | 9 | 6 | 3 |
| 9 | 9 | 7 | 2 |
