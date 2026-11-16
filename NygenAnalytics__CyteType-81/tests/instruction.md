# Issue

**Title:** Marker gene validation

## Description

Implement simple checks on the marker genes before payload construction:

- Check for gene id to gene symbols mapping errors, warning for genes lost in mapping
- Raise value error if marker genes are empty, prevent sending empty marker gene lists
- Validation check if marker genes from adata.uns are gene id like

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7dbb3c55ef6f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.