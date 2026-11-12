# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #396 (id `43240522939`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-11-12T14:45:35Z |
| **Duration** | 9m 47s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 32 (in 10 batch(es))
- **Backup OK**: 15
- **Failed**: 5
- **Partial (fallback / missing data)**: 12
- **Upload failed**: 0
- **Cleanup**: 36 server dir(s) scanned, 15 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 47.115.204.82 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 206.237.13.32 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 46.225.155.61 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| 217.154.254.251 | no matching resource data on server |
| 47.99.187.206 | no matching resource data on server |
| 58.87.67.203 | no matching resource data on server |
| 8.145.62.48 | no matching resource data on server |
| 216.238.121.177 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 96.30.197.163 | no matching resource data on server |
| 84.247.128.146 | no matching resource data on server |
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
| 0 | 4 | 1 | 0 |
| 1 | 4 | 2 | 0 |
| 2 | 4 | 2 | 1 |
| 3 | 4 | 1 | 0 |
| 4 | 4 | 1 | 1 |
| 5 | 4 | 2 | 1 |
| 6 | 4 | 3 | 1 |
| 7 | 4 | 3 | 1 |
| 8 | 0 | 0 | 0 |
| 9 | 0 | 0 | 0 |
