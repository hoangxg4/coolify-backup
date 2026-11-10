# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #390 (id `42734444253`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-11-10T01:15:11Z |
| **Duration** | 10m 11s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 35 (in 10 batch(es))
- **Backup OK**: 15
- **Failed**: 10
- **Partial (fallback / missing data)**: 10
- **Upload failed**: 0
- **Cleanup**: 36 server dir(s) scanned, 12 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 129.121.171.48 | backup failed (ssh rc=255) |
| 47.115.204.82 | backup failed (ssh rc=255) |
| 140.245.209.71 | backup failed (ssh rc=255) |
| 206.237.13.32 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 23.95.86.139 | backup failed (ssh rc=255) |
| 129.121.148.18 | backup failed (ssh rc=124) |
| 144.91.68.178 | backup failed (ssh rc=255) |
| 46.225.155.61 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| 96.30.197.163 | no matching resource data on server |
| 217.154.254.251 | no matching resource data on server |
| 216.238.121.177 | no matching resource data on server |
| 47.99.187.206 | no matching resource data on server |
| 58.87.67.203 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 47.115.201.168 | no matching resource data on server |
| 107.175.127.199 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 140.143.202.209 | no matching resource data on server |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 4 | 2 | 0 |
| 1 | 4 | 1 | 0 |
| 2 | 4 | 2 | 1 |
| 3 | 4 | 1 | 2 |
| 4 | 4 | 0 | 2 |
| 5 | 4 | 2 | 1 |
| 6 | 4 | 3 | 1 |
| 7 | 4 | 3 | 1 |
| 8 | 3 | 1 | 2 |
| 9 | 0 | 0 | 0 |
