# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #52 (id `31300383784`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-08-09T07:06:15Z |
| **Duration** | 16m 43s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 79 (in 10 batch(es))
- **Backup OK**: 61
- **Failed**: 18
- **Partial (data/coolify missing, volumes only)**: 0
- **Upload failed**: 1
- **Cleanup**: 74 server dir(s) scanned, 57 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 209.23.12.105 | backup failed (ssh rc=255) |
| 75.119.149.222 | backup failed (ssh rc=124) |
| 45.77.45.79 | backup failed (ssh rc=255) |
| 173.212.234.212 | backup failed (ssh rc=124) |
| 8.138.177.38 | backup failed (ssh rc=2) |
| 46.225.163.149 | backup failed (ssh rc=255) |
| 209.126.13.81 | backup failed (ssh rc=255) |
| 45.76.20.52 | backup failed (ssh rc=255) |
| 5.129.206.12 | backup failed (ssh rc=124) |
| 13.140.146.212 | backup failed (ssh rc=255) |
| 82.165.41.87 | backup failed (ssh rc=255) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 84.247.168.168 | backup failed (ssh rc=124) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 34.66.134.250 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 149.28.156.246 | backup failed (ssh rc=255) |

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
| 3 | 8 | 5 | 3 |
| 4 | 8 | 6 | 2 |
| 5 | 8 | 8 | 0 |
| 6 | 8 | 4 | 4 |
| 7 | 8 | 6 | 2 |
| 8 | 8 | 6 | 2 |
| 9 | 7 | 6 | 1 |
