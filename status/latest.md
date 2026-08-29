# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #127 (id `33239349081`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-08-29T06:48:13Z |
| **Duration** | 14m 23s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 80 (in 10 batch(es))
- **Backup OK**: 54
- **Failed**: 26
- **Partial (data/coolify missing, volumes only)**: 0
- **Upload failed**: 1
- **Cleanup**: 82 server dir(s) scanned, 51 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 107.175.31.141 | backup failed (ssh rc=255) |
| 173.249.50.12 | backup failed (ssh rc=255) |
| 35.254.77.18 | backup failed (ssh rc=255) |
| 202.182.120.138 | backup failed (ssh rc=255) |
| 75.119.149.222 | backup failed (ssh rc=124) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 43.153.151.229 | backup failed (ssh rc=255) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 8.138.177.38 | backup failed (ssh rc=2) |
| 5.129.206.12 | backup failed (ssh rc=124) |
| 43.139.230.5 | backup failed (ssh rc=255) |
| 46.225.163.149 | backup failed (ssh rc=255) |
| 5.161.237.225 | backup failed (ssh rc=255) |
| 95.217.114.51 | backup failed (ssh rc=255) |
| 173.212.234.212 | backup failed (ssh rc=124) |
| 45.77.45.79 | backup failed (ssh rc=255) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 82.165.41.87 | backup failed (ssh rc=255) |
| 84.247.168.168 | backup failed (ssh rc=255) |
| 5.189.191.35 | backup failed (ssh rc=255) |
| 209.126.13.81 | backup failed (ssh rc=255) |
| 149.28.156.246 | backup failed (ssh rc=255) |
| 82.197.68.176 | backup failed (ssh rc=255) |
| 124.222.18.52 | backup failed (ssh rc=255) |
| 62.113.101.80 | backup failed (ssh rc=255) |

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
| 0 | 8 | 5 | 3 |
| 1 | 8 | 6 | 2 |
| 2 | 8 | 7 | 1 |
| 3 | 8 | 4 | 4 |
| 4 | 8 | 6 | 2 |
| 5 | 8 | 5 | 3 |
| 6 | 8 | 3 | 5 |
| 7 | 8 | 5 | 3 |
| 8 | 8 | 6 | 2 |
| 9 | 8 | 7 | 1 |
