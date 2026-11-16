# Issue

**Title:** fix indexing for larger datasets

## Description

very larger datasets might lead to index overflows. This PR prevent this by moving to 64 bit indexing inside effected kernels

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d46e036e754`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.