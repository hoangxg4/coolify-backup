# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #295 (id `38407253675`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-10-13T13:43:10Z |
| **Duration** | 5m 54s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 30 (in 10 batch(es))
- **Backup OK**: 15
- **Failed**: 7
- **Partial (fallback / missing data)**: 8
- **Upload failed**: 0
- **Cleanup**: 20 server dir(s) scanned, 12 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 158.247.234.240 | backup failed (ssh rc=255) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 154.12.252.216 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 66.253.112.60 | backup failed (ssh rc=255) |
| 130.94.117.183 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| 107.175.127.199 | no matching resource data on server |
| 216.238.121.177 | no matching resource paths, volumes only |
| 194.233.70.145 | no matching resource data on server |
| 23.95.86.139 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 124.174.76.213 | no matching resource data on server |
| 43.134.75.67 | no matching resource paths, volumes only |
| 140.245.209.71 | no matching resource data on server |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 3 | 3 | 0 |
| 1 | 3 | 1 | 1 |
| 2 | 3 | 2 | 1 |
| 3 | 3 | 1 | 0 |
| 4 | 3 | 1 | 1 |
| 5 | 3 | 2 | 1 |
| 6 | 3 | 0 | 2 |
| 7 | 3 | 0 | 1 |
| 8 | 3 | 2 | 0 |
| 9 | 3 | 3 | 0 |
