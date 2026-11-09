# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #388 (id `42564781418`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-11-09T05:00:05Z |
| **Duration** | 9m 46s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 35 (in 10 batch(es))
- **Backup OK**: 16
- **Failed**: 10
- **Partial (fallback / missing data)**: 9
- **Upload failed**: 0
- **Cleanup**: 36 server dir(s) scanned, 13 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 129.121.171.48 | backup failed (ssh rc=255) |
| 140.245.209.71 | backup failed (ssh rc=255) |
| 206.237.13.32 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 47.115.204.82 | backup failed (ssh rc=255) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 107.175.127.199 | backup failed (ssh rc=255) |
| 144.91.68.178 | backup failed (ssh rc=255) |
| 46.225.155.61 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| 216.238.121.177 | no matching resource data on server |
| 47.99.187.206 | no matching resource data on server |
| 58.87.67.203 | no matching resource data on server |
| 217.154.254.251 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 47.115.201.168 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 140.143.202.209 | no matching resource data on server |
| 23.95.86.139 | no matching resource data on server |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 4 | 1 | 0 |
| 1 | 4 | 3 | 0 |
| 2 | 4 | 0 | 2 |
| 3 | 4 | 3 | 0 |
| 4 | 4 | 2 | 2 |
| 5 | 4 | 2 | 1 |
| 6 | 4 | 1 | 2 |
| 7 | 4 | 3 | 1 |
| 8 | 3 | 1 | 2 |
| 9 | 0 | 0 | 0 |
