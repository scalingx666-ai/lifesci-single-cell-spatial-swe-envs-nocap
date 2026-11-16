# Issue

**Title:** fix seurat reference if subset after harmony

## Description

Subsetting Seurat object after running Harmony results in dimension mismatch in obj@reductions$harmony@misc$R because the subset function as implemented in Seurat does not modify the misc slot. This fixes the mismatch by subsetting to the appropriate rows before matmul.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0905e4f17eeb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.