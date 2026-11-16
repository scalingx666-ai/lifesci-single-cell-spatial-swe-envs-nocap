# Issue

**Title:** Fix issue where functions mutate external datasets

## Description

In response to  do not modify variable that is passed into `correct()` or `integrate()`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7502503e9a32`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.