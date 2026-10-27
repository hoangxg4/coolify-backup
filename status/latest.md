# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #349 (id `40498279345`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-10-27T11:43:30Z |
| **Duration** | 12m 59s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 31 (in 10 batch(es))
- **Backup OK**: 12
- **Failed**: 13
- **Partial (fallback / missing data)**: 6
- **Upload failed**: 0
- **Cleanup**: 24 server dir(s) scanned, 12 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 192.99.233.86 | backup failed (ssh rc=124) |
| 140.245.209.71 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 130.94.117.183 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 124.174.76.213 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 185.225.22.210 | backup failed (ssh rc=255) |
| 194.233.70.145 | backup failed (ssh rc=255) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 43.134.75.67 | backup failed (ssh rc=255) |
| 13.140.141.69 | backup failed (ssh rc=255) |
| 144.91.68.178 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| 106.13.5.116 | no matching resource data on server |
| 47.115.201.168 | no matching resource data on server |
| 23.95.86.139 | no matching resource data on server |
| 216.238.121.177 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 107.175.127.199 | no matching resource data on server |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 4 | 2 | 1 |
| 1 | 4 | 2 | 1 |
| 2 | 4 | 1 | 3 |
| 3 | 4 | 3 | 1 |
| 4 | 4 | 0 | 1 |
| 5 | 4 | 1 | 3 |
| 6 | 4 | 2 | 1 |
| 7 | 3 | 1 | 2 |
| 8 | 0 | 0 | 0 |
| 9 | 0 | 0 | 0 |
