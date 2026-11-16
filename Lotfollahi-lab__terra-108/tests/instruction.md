# Issue

**Title:** Feature/cosine gene conflict resolve

## Description

The implementation of cosine similarity between genes can be defined for each combination of cell_gene_ids and neighborhood_gene_ids. It computes the similarity between each pair and stores the results in three arrays under uns with the names: 'sum_cos_sim', 'count', and 'cos_sim' in the given dataset.

To address memory issues, you can set return_gene=False, which will return only the similarity matrix without including the gene-level embedding. for return_gene for neighborhood it will average embedding of genes for that neighborhood.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca21c285e282`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.