# Issue

**Title:** PrepDR5 with BPCells remove dense matrix conversion

## Description

I think this is the likely culprit for issue #8391.

The problem here is that `PrepDR5` has a check to remove features which have the same value for every cell (i.e. have zero variance). Unfortunately, the way it does this causes BPCells matrices to be converted to dense matrices in memory. This change instead uses the variance function provided by BPCells which can operate fully disk-backed.

This means that RunPCA effectively does not get any memory-usage benefit from using BPCells, since PrepDR5 will unnecessarily convert the whole scale.data matrix in-memory. 

With this fix, the RunPCA function should be able to use consistently low memory for BPCells-enabled Seurat objects.

My guess is that the crashes from issue #8391 are people with large datasets running out of memory due to this small oversight in PrepDR5.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21f82c81dc40`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.