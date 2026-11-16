# Issue

**Title:** Add code to work with both zarr 2 and 3, add tests

## Description

- Added version checking for zarr v2 versus v3 and adapt the code in zarr_dataset.py to work with both.
- Added tests for checking zarr API.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b270c9c8843`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.