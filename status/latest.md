# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #43 (id `31133606713`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-08-07T00:09:04Z |
| **Duration** | 14m 37s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 78 (in 10 batch(es))
- **Backup OK**: 65
- **Failed**: 13
- **Partial (data/coolify missing, volumes only)**: 0
- **Upload failed**: 1
- **Cleanup**: 71 server dir(s) scanned, 59 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 75.119.149.222 | backup failed (ssh rc=124) |
| 8.138.177.38 | backup failed (ssh rc=2) |
| 45.77.45.79 | backup failed (ssh rc=255) |
| 209.126.13.81 | backup failed (ssh rc=255) |
| 5.129.206.12 | backup failed (ssh rc=124) |
| 45.76.20.52 | backup failed (ssh rc=255) |
| 13.140.146.212 | backup failed (ssh rc=255) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 34.66.134.250 | backup failed (ssh rc=255) |
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
| 0 | 8 | 8 | 0 |
| 1 | 8 | 8 | 0 |
| 2 | 8 | 7 | 1 |
| 3 | 8 | 7 | 1 |
| 4 | 8 | 5 | 3 |
| 5 | 8 | 7 | 1 |
| 6 | 8 | 7 | 1 |
| 7 | 8 | 4 | 4 |
| 8 | 8 | 7 | 1 |
| 9 | 6 | 5 | 1 |
