# Issue

**Title:** Remove anndata package from dependencies

## Description

Reason: not all users require anndata compatibility, and anndata for R installation not always straightforward (because of reticulate)
Principle: all methods that are using AnnDataR6 are only defined when anndata package is available

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ffa9bc5f8de8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.