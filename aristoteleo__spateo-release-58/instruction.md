# Issue

**Title:** Cluster yao

## Description

Update the cluster function based on dynamo and spagcn.

Add the function for normalization via pysctansform.
Added the function to remove batch effects via harmony.
Added the function to calculate the number of principal components retained.
Add the function to calculate the silhouette coefficient, which is used to evaluate whether the resolution used by the clustering is suitable.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a33f650bd82`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.