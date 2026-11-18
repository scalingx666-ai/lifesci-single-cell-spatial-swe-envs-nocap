# Issue

**Title:** keep psbulk stats when converting to MuData

## Description

- adds data frame to .uns of MuData, which contains the number of cells and counts per view
- stats come from pseudobulk function from decoupler and were stored in `adata.obs`
- previous behaviour was to delete all obs and these stats

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db3a84873177`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.