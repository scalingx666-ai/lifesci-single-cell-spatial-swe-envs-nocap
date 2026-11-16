# Issue

**Title:** Debug `cell_growth_rate()`

## Description

`source` and `target` parameter should be the values in `adata.obs[group]`. Besides, both of them should be optional arguments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e8ffe4a103e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.