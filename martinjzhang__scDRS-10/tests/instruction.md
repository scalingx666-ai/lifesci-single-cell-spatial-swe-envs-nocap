# Issue

**Title:** Unit test

## Description

1. Reorganized files in ./tests 
2. Added tests in ./tests/test_pp.py for scdrs.pp
3. Made minor changes to  scdrs.pp._get_mean_var_implicit_cov_corr and scdrs.method._compute_raw_score to alignt cells, genes, covs before computation
4. Add code to infer n_chunk based on sparsity for scdrs.pp._get_mean_var_implicit_cov_corr
5. Fixing a few minor bugs for type conversion. 
6. There seems to be a merge conflict. Therefore, I suggest to merge this first before adding more unit tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2d9b19719bf9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.