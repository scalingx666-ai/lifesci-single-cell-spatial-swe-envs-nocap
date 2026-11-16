# Issue

**Title:** add the logging info when X_pca, X_umap are added to adata.obsm

## Description

add a log_level parameter to the info_insert_adata function so that we can dynamically set the log level to be printed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4c704663079`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.