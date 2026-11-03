# Coolify Backup - Status Report

| | |
|---|---|
| **Run** | #370 (id `41554346196`) |
| **Trigger** | scheduled (every 6h) |
| **Started** | 2026-11-03T00:38:54Z |
| **Duration** | 10m 05s |
| **Result** | :warning: PARTIAL |
| **API resource mapping** | unavailable (full-backup fallback) |

## Summary

- **Servers**: 30 (in 10 batch(es))
- **Backup OK**: 0
- **Failed**: 14
- **Partial (fallback / missing data)**: 16
- **Upload failed**: 0
- **Cleanup**: 31 server dir(s) scanned, 10 old backup(s) deleted

## Failed hosts

| Host | Reason |
|---|---|
| 140.245.209.71 | backup failed (ssh rc=255) |
| 130.94.117.183 | backup failed (ssh rc=255) |
| 66.97.33.5 | backup failed (ssh rc=255) |
| 203.86.236.158 | backup failed (ssh rc=255) |
| 192.99.233.86 | backup failed (ssh rc=255) |
| 124.174.76.213 | backup failed (ssh rc=255) |
| 13.140.162.90 | backup failed (ssh rc=124) |
| 50.6.240.88 | backup failed (ssh rc=124) |
| 62.146.170.58 | backup failed (ssh rc=255) |
| 103.174.51.37 | backup failed (ssh rc=124) |
| 13.140.141.69 | backup failed (ssh rc=255) |
| 185.98.138.12 | backup failed (ssh rc=124) |
| 144.91.68.178 | backup failed (ssh rc=255) |
| 46.225.155.61 | backup failed (ssh rc=124) |

## Partial backups

| Host | Reason |
|---|---|
| 217.154.254.251 | no resource mapping: full backup |
| 216.238.121.177 | no resource mapping: full backup |
| 159.69.41.211 | no resource mapping: full backup |
| 185.225.22.208 | no resource mapping: full backup |
| 106.13.5.116 | no resource mapping: full backup |
| 47.115.201.168 | no resource mapping: full backup |
| 185.225.22.198 | no resource mapping: full backup |
| 141.145.217.251 | no resource mapping: full backup |
| 15.235.208.191 | no resource mapping: full backup |
| 23.95.86.139 | no resource mapping: full backup |
| 212.83.42.84 | no resource mapping: full backup |
| 137.74.44.1 | no resource mapping: full backup |
| 107.175.127.199 | no resource mapping: full backup |
| 101.34.89.52 | no resource mapping: full backup |
| 129.121.148.18 | no resource mapping: full backup |
| 35.247.190.160 | no resource mapping: full backup |

## Upload failures

| Host | Reason |
|---|---|
| - | None |

## Per-batch

| Batch | Total | OK | Failed |
|---|---|---|---|
| 0 | 3 | 0 | 0 |
| 1 | 3 | 0 | 1 |
| 2 | 3 | 0 | 2 |
| 3 | 3 | 0 | 2 |
| 4 | 3 | 0 | 1 |
| 5 | 3 | 0 | 0 |
| 6 | 3 | 0 | 2 |
| 7 | 3 | 0 | 2 |
| 8 | 3 | 0 | 2 |
| 9 | 3 | 0 | 2 |
