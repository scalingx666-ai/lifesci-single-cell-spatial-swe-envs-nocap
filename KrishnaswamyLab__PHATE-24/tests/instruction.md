# Issue

**Title:** Upgrade to version 0.2.4: accepts affinity and distance matrices

## Description

If `knn_dist` is 'precomputed', then 'data' can be either a distance matrix (all zeros along diagonal) or an affinity matrix (all non-zeroes along diagonal.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9804d9d62b37`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.