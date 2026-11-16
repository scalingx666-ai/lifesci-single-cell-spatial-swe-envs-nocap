# Issue

**Title:** Add linear regression for `IterableMatrix`

## Description

Hi, @bnprks,

I finally get `LinearResidual` works correctly. This idea was generally inspired from [ResidualMatrix](https://bioconductor.org/packages/3.19/bioc/html/ResidualMatrix.html) package.

A new test has been added to `test-matrix_transforms.R` to make sure `linear_regress_out` get the same results compared to `Seurat:::RegressOutMatrix`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee75a6b2e8e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.