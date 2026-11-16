# Issue

**Title:** Allow to merge a bc object to its own subset

## Description

In case `bc1` is a subset of `bc2`, the merged object will contain only the cells present in `bc1` and all signatures in `bc1` and `bc2`. The `SeuratInfo` of the resulting object will be the same as in `bc1`. The clusters and ranks must be recomputed after the merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `046f58c716b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.