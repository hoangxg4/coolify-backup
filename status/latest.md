# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #359 (id `41054199348`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-10-30T12:17:15Z |
| **Duration** | 15m 30s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 30 (in 10 batch(es))
- **Backup OK**: 12
- **Failed**: 11
- **Partial (fallback / missing data)**: 7
- **Upload failed**: 1
- **Cleanup**: 25 server dir(s) scanned, 11 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 140.245.209.71 | backup failed (ssh rc=255) |
| 124.174.76.213 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 130.94.117.183 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 144.91.68.178 | backup failed (ssh rc=255) |
| 185.98.138.12 | backup failed (ssh rc=124) |
| 13.140.141.69 | backup failed (ssh rc=255) |
| 46.225.155.61 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| 217.154.254.251 | no matching resource data on server |
| 106.13.5.116 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 47.115.201.168 | no matching resource data on server |
| 216.238.121.177 | no matching resource data on server |
| 23.95.86.139 | no matching resource data on server |
| 107.175.127.199 | no matching resource data on server |

## Upload failures

| Host | Reason |
|---|---|
| 192.99.233.86 | rclone copy failed |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 3 | 2 | 0 |
| 1 | 3 | 1 | 1 |
| 2 | 3 | 1 | 1 |
| 3 | 3 | 0 | 2 |
| 4 | 3 | 2 | 1 |
| 5 | 3 | 2 | 0 |
| 6 | 3 | 1 | 1 |
| 7 | 3 | 1 | 1 |
| 8 | 3 | 1 | 2 |
| 9 | 3 | 1 | 2 |
