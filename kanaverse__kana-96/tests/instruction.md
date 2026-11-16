# Issue

**Title:** Switch to PCA partitioning for k-means initialization.

## Description

Depends on jkanche/scran.js#36.

I'm thinking we should also add a UI option to set the seed, given how sensitive k-means is to the initialization process. (Depending on how that goes, we might consider adding a similar option to t-SNE and UMAP, so people can play around with the seed and see how their results change.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a71eef14d0af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.