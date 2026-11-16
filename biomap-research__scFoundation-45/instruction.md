# Issue

**Title:** Update get_embedding.py to fix a bug of querying genes

## Description

Hi, in the get_embedding.py code, the gene matching step requires that input h5ad file should have gene_name column, but no explict instructions. I believe most people will store gene names in var_names, so I add another option to avoid potential bugs. Thanks.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9196178d8f6e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.