# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #69 (id `31704934749`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-08-13T13:26:36Z |
| **Duration** | 9m 58s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 74 (in 10 batch(es))
- **Backup OK**: 58
- **Failed**: 15
- **Partial (data/coolify missing, volumes only)**: 1
- **Upload failed**: 0
- **Cleanup**: 74 server dir(s) scanned, 59 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 75.119.149.222 | backup failed (ssh rc=124) |
| 8.138.177.38 | backup failed (ssh rc=2) |
| 46.225.163.149 | backup failed (ssh rc=255) |
| 209.126.13.81 | backup failed (ssh rc=255) |
| 5.129.206.12 | backup failed (ssh rc=124) |
| 82.165.41.87 | backup failed (ssh rc=255) |
| 141.136.44.86 | backup failed (ssh rc=255) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 173.212.234.212 | backup failed (ssh rc=124) |
| 84.247.168.168 | backup failed (ssh rc=124) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 45.77.45.79 | backup failed (ssh rc=255) |
| 149.28.156.246 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| 167.233.120.15 | data/coolify missing, volumes only |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 8 | 8 | 0 |
| 1 | 8 | 7 | 1 |
| 2 | 8 | 8 | 0 |
| 3 | 8 | 4 | 3 |
| 4 | 8 | 7 | 1 |
| 5 | 8 | 6 | 2 |
| 6 | 8 | 4 | 4 |
| 7 | 8 | 5 | 3 |
| 8 | 8 | 8 | 0 |
| 9 | 2 | 1 | 1 |
