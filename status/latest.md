# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #44 (id `31157701521`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-08-07T07:27:08Z |
| **Duration** | 11m 20s |
| **Result** | :warning: PARTIAL |

## Summary

- **Servers**: 75 (in 10 batch(es))
- **Backup OK**: 60
- **Failed**: 15
- **Partial (data/coolify missing, volumes only)**: 0
- **Upload failed**: 0
- **Cleanup**: 71 server dir(s) scanned, 55 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 209.23.12.105 | backup failed (ssh rc=255) |
| 75.119.149.222 | backup failed (ssh rc=124) |
| 8.138.177.38 | backup failed (ssh rc=2) |
| 209.126.13.81 | backup failed (ssh rc=255) |
| 45.77.45.79 | backup failed (ssh rc=255) |
| 45.76.20.52 | backup failed (ssh rc=255) |
| 5.129.206.12 | backup failed (ssh rc=124) |
| 13.140.146.212 | backup failed (ssh rc=255) |
| 52.18.184.32 | backup failed (ssh rc=255) |
| 141.136.44.86 | backup failed (ssh rc=255) |
| 176.31.163.96 | backup failed (ssh rc=255) |
| 178.156.235.241 | backup failed (ssh rc=255) |
| 136.116.116.216 | backup failed (ssh rc=255) |
| 34.66.134.250 | backup failed (ssh rc=255) |
| 149.28.156.246 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| - | None |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 8 | 7 | 1 |
| 1 | 8 | 7 | 1 |
| 2 | 8 | 7 | 1 |
| 3 | 8 | 6 | 2 |
| 4 | 8 | 6 | 2 |
| 5 | 8 | 7 | 1 |
| 6 | 8 | 6 | 2 |
| 7 | 8 | 5 | 3 |
| 8 | 8 | 7 | 1 |
| 9 | 3 | 2 | 1 |
