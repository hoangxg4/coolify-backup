# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #85 (id `32032395720`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-08-17T12:56:30Z |
| **Duration** | 16m 08s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 77 (in 10 batch(es))
- **Backup OK**: 59
- **Failed**: 18
- **Partial (data/coolify missing, volumes only)**: 0
- **Upload failed**: 2
- **Cleanup**: 77 server dir(s) scanned, 57 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 3.65.136.33 | backup failed (ssh rc=255) |
| 173.249.50.12 | backup failed (ssh rc=255) |
| 75.119.149.222 | backup failed (ssh rc=124) |
| 63.181.121.248 | backup failed (ssh rc=255) |
| 8.138.177.38 | backup failed (ssh rc=2) |
| 209.126.13.81 | backup failed (ssh rc=255) |
| 149.28.156.246 | backup failed (ssh rc=255) |
| 203.175.10.199 | backup failed (ssh rc=255) |
| 5.129.206.12 | backup failed (ssh rc=124) |
| 46.225.163.149 | backup failed (ssh rc=255) |
| 141.136.44.86 | backup failed (ssh rc=255) |
| 82.165.41.87 | backup failed (ssh rc=255) |
| 173.212.234.212 | backup failed (ssh rc=124) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 45.77.45.79 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| - | None |

## Upload failures

| Host | Reason |
|---|---|
| 84.247.168.168 | rclone copy failed |
| 62.238.41.18 | rclone copy failed |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 8 | 6 | 2 |
| 1 | 8 | 7 | 1 |
| 2 | 8 | 7 | 1 |
| 3 | 8 | 5 | 3 |
| 4 | 8 | 6 | 2 |
| 5 | 8 | 7 | 1 |
| 6 | 8 | 5 | 3 |
| 7 | 8 | 3 | 5 |
| 8 | 8 | 8 | 0 |
| 9 | 5 | 5 | 0 |
