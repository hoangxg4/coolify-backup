# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #398 (id `43372293316`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-11-13T05:28:54Z |
| **Duration** | 6m 32s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 32 (in 10 batch(es))
- **Backup OK**: 12
- **Failed**: 8
- **Partial (fallback / missing data)**: 12
- **Upload failed**: 0
- **Cleanup**: 36 server dir(s) scanned, 12 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 206.237.13.32 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 47.115.204.82 | backup failed (ssh rc=255) |
| 43.135.10.205 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 35.247.190.160 | backup failed (ssh rc=255) |
| 46.225.155.61 | backup failed (ssh rc=124) |
| 129.121.148.18 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| 217.154.254.251 | no matching resource data on server |
| 47.99.187.206 | no matching resource data on server |
| 58.87.67.203 | no matching resource data on server |
| 216.238.121.177 | no matching resource data on server |
| 8.145.62.48 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 84.247.128.146 | no matching resource data on server |
| 47.115.201.168 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 107.175.127.199 | no matching resource data on server |
| 96.30.197.163 | no matching resource data on server |
| 140.143.202.209 | no matching resource data on server |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 4 | 1 | 0 |
| 1 | 4 | 3 | 0 |
| 2 | 4 | 2 | 0 |
| 3 | 4 | 1 | 0 |
| 4 | 4 | 1 | 2 |
| 5 | 4 | 1 | 1 |
| 6 | 4 | 2 | 2 |
| 7 | 4 | 1 | 3 |
| 8 | 0 | 0 | 0 |
| 9 | 0 | 0 | 0 |
