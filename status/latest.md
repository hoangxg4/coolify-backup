# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #339 (id `40107320887`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-10-24T15:30:55Z |
| **Duration** | 10m 10s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 31 (in 10 batch(es))
- **Backup OK**: 12
- **Failed**: 14
- **Partial (fallback / missing data)**: 5
- **Upload failed**: 0
- **Cleanup**: 24 server dir(s) scanned, 12 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 140.245.209.71 | backup failed (ssh rc=255) |
| 130.94.117.183 | backup failed (ssh rc=255) |
| 192.99.233.86 | backup failed (ssh rc=124) |
| 101.34.89.52 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 124.174.76.213 | backup failed (ssh rc=255) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 194.233.70.145 | backup failed (ssh rc=255) |
| 43.134.75.67 | backup failed (ssh rc=255) |
| 103.174.51.37 | backup failed (ssh rc=124) |
| 13.140.141.69 | backup failed (ssh rc=255) |
| 144.91.68.178 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
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
| 0 | 4 | 1 | 3 |
| 1 | 4 | 1 | 2 |
| 2 | 4 | 3 | 0 |
| 3 | 4 | 2 | 2 |
| 4 | 4 | 1 | 2 |
| 5 | 4 | 2 | 1 |
| 6 | 4 | 1 | 2 |
| 7 | 3 | 1 | 2 |
| 8 | 0 | 0 | 0 |
| 9 | 0 | 0 | 0 |
