# Issue

**Title:** bump mins: python, spatialdata, dask

## Description

Requires 

Todo:
- [x] bump min spatialdata version to 0.7.0

Should fix the install problem  reported by @tischi

---
This PR also removes the benchmarks job from `test.yaml`. The rationale behind this is discussed here:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c95e3e271184`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.