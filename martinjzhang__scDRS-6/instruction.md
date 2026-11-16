# Issue

**Title:** Gene weights

## Description

Move gene set reading and processing into function `scdrs.util.load_gs`. This function handles
1. Read .gs file, support both old version of gene sets or gene sets with continuous weights.
2. Convert to homolog genes between mouse and human if needed.
3. Overlap with the prespecified set of genes, e.g., adata.var_names if needed.

Corresponding tests are also added.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a88c3627f03c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.