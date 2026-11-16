# Issue

**Title:** convert adata.X to csc matrix for compute raw score speed up

## Description

I convert the adata.X from a csr matrix to a csc sparse matrix to speed up subsetting the matrix by genes.

Note: I only do this for the normal mode, so if the flag_sparse and flag_cov are True, then the csr matrix is not used. Additionally I have not made any changes to _compute_overdispersion_score. This is because I don't know how to test this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc1e77b58ec5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.