# Issue

**Title:** Driver genes update

## Description

Updates:
- Added compute_driver_genes function in utils_via.py
- Updated get_gene_expression function to give the option to directly call compute_driver_genes and plot top 5 driver gene expressions of each terminal states.
- Also added a confidence interval to the gene expression plot.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e27f77d65e69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.