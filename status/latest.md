# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #384 (id `42416237049`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-11-07T21:31:10Z |
| **Duration** | 9m 05s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 34 (in 10 batch(es))
- **Backup OK**: 13
- **Failed**: 12
- **Partial (fallback / missing data)**: 9
- **Upload failed**: 0
- **Cleanup**: 33 server dir(s) scanned, 13 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 129.121.171.48 | backup failed (ssh rc=255) |
| 130.94.117.183 | backup failed (ssh rc=255) |
| 140.245.209.71 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 192.99.233.86 | backup failed (ssh rc=255) |
| 47.115.204.82 | backup failed (ssh rc=255) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 107.175.127.199 | backup failed (ssh rc=255) |
| 144.91.68.178 | backup failed (ssh rc=255) |
| 46.225.155.61 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| 217.154.254.251 | no matching resource data on server |
| 216.238.121.177 | no matching resource data on server |
| 47.99.187.206 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 58.87.67.203 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 47.115.201.168 | no matching resource data on server |
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
| 1 | 4 | 2 | 0 |
| 2 | 4 | 1 | 3 |
| 3 | 4 | 2 | 0 |
| 4 | 4 | 1 | 3 |
| 5 | 4 | 2 | 1 |
| 6 | 4 | 1 | 2 |
| 7 | 4 | 2 | 2 |
| 8 | 2 | 1 | 1 |
| 9 | 0 | 0 | 0 |
