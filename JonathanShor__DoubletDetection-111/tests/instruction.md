# Issue

**Title:** Dev v2.4

## Description

- Adds random state parameter for PCA, tSNE, synthetic doublet creation in BoostClassifer -  
- Adds random state parameter for PCA, tSNE in tsne plot
- tsne plot returns PhenoGraph communities -  
- tsne plot accepts array-like through sklearn check array -  
- improves readability of threshold plot -  
- notebook uses voter threshold of 0.8 (non-default)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d807facd40a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.