# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #372 (id `41735265919`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-11-03T22:57:58Z |
| **Duration** | 10m 43s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 32 (in 10 batch(es))
- **Backup OK**: 13
- **Failed**: 12
- **Partial (fallback / missing data)**: 7
- **Upload failed**: 0
- **Cleanup**: 32 server dir(s) scanned, 12 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 129.121.171.48 | backup failed (ssh rc=255) |
| 140.245.209.71 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 130.94.117.183 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 192.99.233.86 | backup failed (ssh rc=255) |
| 124.174.76.213 | backup failed (ssh rc=255) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 13.140.141.69 | backup failed (ssh rc=255) |
| 144.91.68.178 | backup failed (ssh rc=255) |
| 46.225.155.61 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| 216.238.121.177 | no matching resource data on server |
| 217.154.254.251 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 47.115.201.168 | no matching resource data on server |
| 23.95.86.139 | no matching resource data on server |
| 107.175.127.199 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 4 | 2 | 1 |
| 1 | 4 | 1 | 1 |
| 2 | 4 | 1 | 2 |
| 3 | 4 | 2 | 2 |
| 4 | 4 | 2 | 1 |
| 5 | 4 | 1 | 2 |
| 6 | 4 | 3 | 0 |
| 7 | 4 | 1 | 3 |
| 8 | 0 | 0 | 0 |
| 9 | 0 | 0 | 0 |
