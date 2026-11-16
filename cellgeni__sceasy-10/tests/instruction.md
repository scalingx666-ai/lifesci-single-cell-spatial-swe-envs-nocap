# Issue

**Title:** Enable anndata to seurat conversion

## Description

Add anndata and seurat to permitted to/from strings.

Fix return type of obsm.keys() so it returns a list of strings instead of a KeysView object.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `48b9f12e2b84`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.