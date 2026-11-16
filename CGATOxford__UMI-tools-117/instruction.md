# Issue

**Title:** Code algos in c

## Description

This merge brings in the separation of read grouping and read deduplication as implemented by @IanSudbery as the first step in transcoding the network functions into a C library. 

The changes in the adjacency method alter the output order.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9de02901432f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.