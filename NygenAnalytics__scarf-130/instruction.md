# Issue

**Title:** CrDirReader Update [Polars -> Pandas]

## Description

# CrDirReader Update

The current version encountered issues with reading compressed files via `polars`, which caused high memory usage by attempting to decompress files entirely in memory. This update rolls back to `pandas` for reading files in manageable chunks.

Key changes:
- Reverted to `pandas` for chunked reading to handle compressed files more efficiently.
- Processes chunks in `pandas` and applies `_get_valid_barcodes()` when `is_filtered` is set to `False`.

This ensures lower memory usage and more reliable processing of large datasets.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edca2ed860f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.