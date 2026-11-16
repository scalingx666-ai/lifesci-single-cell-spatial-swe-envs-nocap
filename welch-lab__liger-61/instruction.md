# Issue

**Title:** Fix switching of cell names for empty cells in merge

## Description

This bug would only affect the merging of datasets which did not have a min UMI cutoff, and where cell-name needed to be consistent across multiple clustering analyses.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d7c8dc1cba4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.