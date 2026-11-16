# Issue

**Title:** Round 2: doubletCluster

## Description

Migrated `scran::doubletCluster` into this package as `findDoubletClusters()`.

I created a new vignette with a quick real-data example and a lot of the theoretical background. This pulls in **scRNAseq** as a new `Suggests:`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2188ba9eda9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.