# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #326 (id `39607708351`) |
| **Trigger** | manual |
| **Started** | 2026-10-21T13:24:24Z |
| **Duration** | 6m 15s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 31 (in 10 batch(es))
- **Backup OK**: 15
- **Failed**: 8
- **Partial (fallback / missing data)**: 8
- **Upload failed**: 0
- **Cleanup**: 23 server dir(s) scanned, 16 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 192.99.233.86 | backup failed (ssh rc=124) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 124.174.76.213 | backup failed (ssh rc=255) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 130.94.117.183 | backup failed (ssh rc=255) |
| 194.233.70.145 | backup failed (ssh rc=255) |
| 144.91.68.178 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| 47.115.201.168 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 140.245.209.71 | no matching resource data on server |
| 23.95.86.139 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 216.238.121.177 | no matching resource paths, volumes only |
| 107.175.127.199 | no matching resource data on server |
| 43.134.75.67 | no matching resource paths, volumes only |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 4 | 3 | 1 |
| 1 | 4 | 2 | 0 |
| 2 | 4 | 2 | 2 |
| 3 | 4 | 0 | 3 |
| 4 | 4 | 1 | 0 |
| 5 | 4 | 1 | 1 |
| 6 | 4 | 4 | 0 |
| 7 | 3 | 2 | 1 |
| 8 | 0 | 0 | 0 |
| 9 | 0 | 0 | 0 |
