# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #32 (id `30874551258`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-08-04T03:22:09Z |
| **Duration** | 19m 33s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 74 (in 10 batch(es))
- **Backup OK**: 58
- **Failed**: 16
- **Partial (data/coolify missing, volumes only)**: 0
- **Upload failed**: 2
- **Cleanup**: 66 server dir(s) scanned, 56 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 212.115.125.196 | backup failed (ssh rc=255) |
| 75.119.149.222 | backup failed (ssh rc=124) |
| 203.175.10.199 | backup failed (ssh rc=255) |
| 45.76.20.52 | backup failed (ssh rc=255) |
| 8.138.177.38 | backup failed (ssh rc=255) |
| 45.77.45.79 | backup failed (ssh rc=255) |
| 209.126.13.81 | backup failed (ssh rc=255) |
| 5.129.206.12 | backup failed (ssh rc=124) |
| 13.140.146.212 | backup failed (ssh rc=255) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 103.40.161.174 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 143.198.180.207 | backup failed (ssh rc=255) |
| 149.28.156.246 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| - | None |

## Upload failures

| Host | Reason |
|---|---|
| 176.9.89.217 | rclone copy failed |
| 62.238.41.18 | rclone copy failed |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 8 | 7 | 1 |
| 1 | 8 | 7 | 1 |
| 2 | 8 | 6 | 2 |
| 3 | 8 | 7 | 1 |
| 4 | 8 | 5 | 3 |
| 5 | 8 | 7 | 1 |
| 6 | 8 | 5 | 3 |
| 7 | 8 | 6 | 2 |
| 8 | 8 | 7 | 1 |
| 9 | 2 | 1 | 1 |
