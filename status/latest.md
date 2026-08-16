# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #80 (id `31932426490`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-08-16T06:51:26Z |
| **Duration** | 14m 23s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 77 (in 10 batch(es))
- **Backup OK**: 61
- **Failed**: 16
- **Partial (data/coolify missing, volumes only)**: 0
- **Upload failed**: 1
- **Cleanup**: 77 server dir(s) scanned, 57 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 173.249.50.12 | backup failed (ssh rc=255) |
| 75.119.149.222 | backup failed (ssh rc=124) |
| 203.175.10.199 | backup failed (ssh rc=255) |
| 5.189.191.35 | backup failed (ssh rc=255) |
| 8.138.177.38 | backup failed (ssh rc=2) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 149.28.156.246 | backup failed (ssh rc=255) |
| 173.212.234.212 | backup failed (ssh rc=124) |
| 209.126.13.81 | backup failed (ssh rc=255) |
| 5.129.206.12 | backup failed (ssh rc=124) |
| 46.225.163.149 | backup failed (ssh rc=255) |
| 82.165.41.87 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 45.77.45.79 | backup failed (ssh rc=255) |

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
| 0 | 8 | 7 | 1 |
| 1 | 8 | 7 | 1 |
| 2 | 8 | 6 | 2 |
| 3 | 8 | 4 | 4 |
| 4 | 8 | 6 | 2 |
| 5 | 8 | 7 | 1 |
| 6 | 8 | 7 | 1 |
| 7 | 8 | 4 | 4 |
| 8 | 8 | 8 | 0 |
| 9 | 5 | 5 | 0 |
