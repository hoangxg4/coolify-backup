# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #290 (id `38138553473`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-10-11T12:15:09Z |
| **Duration** | 7m 31s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 25 (in 10 batch(es))
- **Backup OK**: 13
- **Failed**: 6
- **Partial (fallback / missing data)**: 6
- **Upload failed**: 0
- **Cleanup**: 15 server dir(s) scanned, 0 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 118.25.191.55 | backup failed (ssh rc=255) |
| 158.247.234.240 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 154.12.252.216 | backup failed (ssh rc=255) |
| 66.253.112.60 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| 216.238.121.177 | no matching resource paths, volumes only |
| 194.233.70.145 | no matching resource data on server |
| 140.245.209.71 | no matching resource data on server |
| 101.34.89.52 | no matching resource data on server |
| 43.134.75.67 | no matching resource paths, volumes only |
| 124.174.76.213 | no matching resource data on server |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 3 | 1 | 1 |
| 1 | 3 | 2 | 1 |
| 2 | 3 | 3 | 0 |
| 3 | 3 | 0 | 0 |
| 4 | 3 | 2 | 1 |
| 5 | 3 | 0 | 3 |
| 6 | 3 | 2 | 0 |
| 7 | 3 | 2 | 0 |
| 8 | 1 | 1 | 0 |
| 9 | 0 | 0 | 0 |
