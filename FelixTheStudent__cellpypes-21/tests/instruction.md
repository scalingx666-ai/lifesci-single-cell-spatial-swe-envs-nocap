# Issue

**Title:** Allow NA expr

## Description

I had one data set in which totalUMIs were 0 for some cells. This led to NAs for ALL CELLS WITH 0 UMIs. Here I fix this with min(..., na.rm=TRUE).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae0c800abdc2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.