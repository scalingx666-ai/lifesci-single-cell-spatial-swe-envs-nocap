# Issue

**Title:** h5ad lower RAM

## Description

Slightly modified h5ad code to lower RAM spike when dealing with a large number of genes (loaded in the index as string type rather than manual conversion later loading).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `786b2e1772df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.