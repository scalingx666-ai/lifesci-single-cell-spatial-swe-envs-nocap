# Issue

**Title:** img-workflow-xenium

## Description

1st draft based on Estella's BC2 workshop, but not using `Seurat`... Data retrieval from OSF works, but `SpatialExperimentIO` needs updating to recognize `cells.parquet`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d59a35003bad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.