# Issue

**Title:** Don't assert for index/column names when comparing series (e.g. in `set_x`, `set_y`, and `set_x`)

## Description

Fixes  To standardize series assertions I used an utility function in all cases where `pd.testing.assert_equal_series` is used.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `939e91bef0e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.