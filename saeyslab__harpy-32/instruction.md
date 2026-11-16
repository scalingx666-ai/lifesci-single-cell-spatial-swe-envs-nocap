# Issue

**Title:** Sc 10 allocation issue

## Description

- sparse coo matrix instead of unstack in allocation
- delayed query of dask dataframe in allocation step for speedup

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cde933ee8110`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.