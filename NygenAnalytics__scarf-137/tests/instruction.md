# Issue

**Title:** DatasetMerge fix

## Description

Resolved critical error when performing `DatasetMerge`. The previous merging caused cell indices to get mixed.

Working example

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d1c8deb5d32b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.