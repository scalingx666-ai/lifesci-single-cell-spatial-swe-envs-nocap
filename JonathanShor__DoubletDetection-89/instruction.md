# Issue

**Title:** Dev v2.1

## Description

- Adds plotting capabilities to monitor convergence and view predicted doublets on tSNE

- Disables downsampling by default

- Adds loading methods for mtx and 10x h5 format

- Enables input of sparse matrices, pandas DFs, etc.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3bc065e77b80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.