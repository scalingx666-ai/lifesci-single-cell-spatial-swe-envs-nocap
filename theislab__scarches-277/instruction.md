# Issue

**Title:** Remove deprecated anndata.read imports and replace with anndat.read_h5ad

## Description

Fixing: 

When using scarches with a newer version of anndata 

`ImportError: cannot import name 'read' from 'anndata'`

Two of the imports were unused anyways.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88b19dceaec6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.