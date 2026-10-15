# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #303 (id `38769189645`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-10-15T16:27:46Z |
| **Duration** | 6m 00s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 33 (in 10 batch(es))
- **Backup OK**: 16
- **Failed**: 7
- **Partial (fallback / missing data)**: 10
- **Upload failed**: 0
- **Cleanup**: 22 server dir(s) scanned, 18 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 158.247.234.240 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 130.94.117.183 | backup failed (ssh rc=255) |
| 154.12.252.216 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 66.253.112.60 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| 216.238.121.177 | no matching resource paths, volumes only |
| 124.174.76.213 | no matching resource data on server |
| 47.115.201.168 | no matching resource data on server |
| 140.245.209.71 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 23.95.86.139 | no matching resource data on server |
| 107.175.127.199 | no matching resource data on server |
| 194.233.70.145 | no matching resource data on server |
| 43.134.75.67 | no matching resource paths, volumes only |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 4 | 3 | 1 |
| 1 | 4 | 3 | 1 |
| 2 | 4 | 1 | 1 |
| 3 | 4 | 1 | 1 |
| 4 | 4 | 2 | 1 |
| 5 | 4 | 1 | 2 |
| 6 | 4 | 1 | 0 |
| 7 | 4 | 3 | 0 |
| 8 | 1 | 1 | 0 |
| 9 | 0 | 0 | 0 |
