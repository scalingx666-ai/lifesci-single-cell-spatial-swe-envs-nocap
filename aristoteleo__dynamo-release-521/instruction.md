# Issue

**Title:** update normalization default parameters

## Description

Update normalize parameters to reproduce the results of the recipe monocle.

- round_exprs should be True
- total_szfactor should be None. When normalizing label data by total size factors, we need to set the parameter explicitly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `beaf71a6fd47`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.