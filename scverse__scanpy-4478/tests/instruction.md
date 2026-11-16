# Issue

**Title:** Backport PR #4446 on branch 1.12.x (fix: avoid loading whole dask arrays in `axis_nnz` and `check_nonnegative_integers`)

## Description

Backport PR #4446: fix: avoid loading whole dask arrays in `axis_nnz` and `check_nonnegative_integers`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e1877506505`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.