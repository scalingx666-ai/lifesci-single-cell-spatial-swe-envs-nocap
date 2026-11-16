# Issue

**Title:** Fix definition of `n_jobs`

## Description

## Bug fixes

* `n_jobs` can now be given as an arbitrary integer.

## New

* The function `get_n_jobs` is added updates the number of jobs `n_jobs` to the expected format.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `329281e33e2e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.