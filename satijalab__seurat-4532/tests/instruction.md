# Issue

**Title:** Bugfix to as.SingleCellExperiment

## Description

This is related to the issue I opened here:   which includes a simple repro case.

Whenever I run as.SingleCellExperiment(), it gives errors like this:

Error in value[3L] :
invalid subscript 'e' in 'altExp(, type="character", ...)':
'RNA' not in 'altExpNames()'

I believe the issue is that the 4.0.2 version of as.SingleCellExperiment tries to call SingleCellExperiment::swapAltExp() when passing the name of the currently active experiment. 

I think that worked in as.Seurat.SingleCellExperiment(), since you inject "originalexp" into the object, so iterating the true assay names works.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af2925ce71f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.