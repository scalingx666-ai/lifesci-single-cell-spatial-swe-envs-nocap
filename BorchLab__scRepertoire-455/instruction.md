# Issue

**Title:** fix shuffling of cell barcodes in SingleCellExperiment object

## Description

Update combineExpression.R to get rid of the line that causes shuffling of the row names

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `08e80abcaf1e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.