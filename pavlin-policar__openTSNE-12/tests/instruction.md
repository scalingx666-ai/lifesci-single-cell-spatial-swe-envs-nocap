# Issue

**Title:** Properly handle negative values of n_jobs

## Description

: Properly handle negative values of the  `n_jobs` parameter in the same way sklearn does.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ede566f7ba41`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.