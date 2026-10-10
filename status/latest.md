# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #286 (id `38052179133`) |
| **Trigger** | manual |
| **Started** | 2026-10-10T12:30:05Z |
| **Duration** | 5m 09s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | OK (resource-filtered) |

## Summary

- **Servers**: 25 (in 10 batch(es))
- **Backup OK**: 13
- **Failed**: 6
- **Partial (fallback / missing data)**: 6
- **Upload failed**: 0
- **Cleanup**: skipped (RCLONE_REMOTE misconfigured)

## Failed hosts

| Host | Reason |
|---|---|
| 118.25.191.55 | backup failed (ssh rc=255) |
| 66.253.112.60 | backup failed (ssh rc=255) |
| 158.247.234.240 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 154.12.252.216 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |

## Partial backups

| Host | Reason |
|---|---|
| 216.238.121.177 | no matching resource paths, volumes only |
| 101.34.89.52 | no matching resource data on server |
| 194.233.70.145 | no matching resource data on server |
| 140.245.209.71 | no matching resource data on server |
| 124.174.76.213 | no matching resource data on server |
| 43.134.75.67 | no matching resource paths, volumes only |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 3 | 2 | 1 |
| 1 | 3 | 0 | 2 |
| 2 | 3 | 3 | 0 |
| 3 | 3 | 2 | 0 |
| 4 | 3 | 1 | 2 |
| 5 | 3 | 1 | 0 |
| 6 | 3 | 2 | 1 |
| 7 | 3 | 2 | 0 |
| 8 | 1 | 0 | 0 |
| 9 | 0 | 0 | 0 |
