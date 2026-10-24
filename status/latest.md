# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #338 (id `40085894559`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-10-24T10:26:05Z |
| **Duration** | 7m 49s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 31 (in 10 batch(es))
- **Backup OK**: 13
- **Failed**: 12
- **Partial (fallback / missing data)**: 6
- **Upload failed**: 0
- **Cleanup**: 24 server dir(s) scanned, 13 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 140.245.209.71 | backup failed (ssh rc=255) |
| 192.99.233.86 | backup failed (ssh rc=124) |
| 130.94.117.183 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 194.233.70.145 | backup failed (ssh rc=255) |
| 124.174.76.213 | backup failed (ssh rc=255) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 43.134.75.67 | backup failed (ssh rc=255) |
| 103.174.51.37 | backup failed (ssh rc=124) |
| 13.140.141.69 | backup failed (ssh rc=255) |
| 144.91.68.178 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| 101.34.89.52 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 47.115.201.168 | no matching resource data on server |
| 216.238.121.177 | no matching resource data on server |
| 23.95.86.139 | no matching resource data on server |
| 107.175.127.199 | no matching resource data on server |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 4 | 2 | 2 |
| 1 | 4 | 2 | 0 |
| 2 | 4 | 2 | 1 |
| 3 | 4 | 2 | 2 |
| 4 | 4 | 0 | 3 |
| 5 | 4 | 2 | 0 |
| 6 | 4 | 2 | 2 |
| 7 | 3 | 1 | 2 |
| 8 | 0 | 0 | 0 |
| 9 | 0 | 0 | 0 |
