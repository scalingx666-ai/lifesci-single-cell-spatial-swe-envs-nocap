# Issue

**Title:** Remove `_create_sparse_df` implementation and use public pandas API in ligrec

## Description

This is an alternative solution to the problem in  This also gets rid of `_create_sparse_df` which was a workaround pandas code which will probably age bad since it uses private interfaces and is an old copy of pandas code. It also fixes the the pandas 3.0 compat from the integration tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c112239144e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.