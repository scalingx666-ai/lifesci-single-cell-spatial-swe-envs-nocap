# Issue

**Title:** Implementation of `sc_dot` method

## Description

Thank you for developing this very useful package.

I have implemented the `sc_dot` method for the `Seurat` and `SingleCellExperiment` objects, replicating `Seurat::DotPlot`.


I tried to make the function with the basic functionality of `Seurat::DotPlot`. Some codes are copied and adapted from the `Seurat` codebase. One `Imports` of `RColorBrewer` has been added to DESCRIPTION. R CMD CHECK passed without errors and warnings in R 4.3.1.

I would be grateful if you could review the codes for the possible integration.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af951af41483`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.