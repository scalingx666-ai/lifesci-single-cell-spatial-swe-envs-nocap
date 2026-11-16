# Issue

**Title:** Make HEST-Benchmark deterministic

## Description

- Set seed in PCA, XGBoost and RandomForestRegressor
-  Rm PLIP from bench zoo

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b87046fbcb6e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.