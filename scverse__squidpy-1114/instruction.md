# Issue

**Title:** Lower bound spatialdata>=1.7.1

## Description

Since dask-expr is deprecated there we better ~~lower bound it~~ switch to the version of spatialdata that no longer uses it. It works well with dask this way and doesn't give 

```
dask-expr 1.1.19 requires dask==2024.11.2, but you have dask 2026.1.2 which is incompatible.
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `469a7d079159`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.