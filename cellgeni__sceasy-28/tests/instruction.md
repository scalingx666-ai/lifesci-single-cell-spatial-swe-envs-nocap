# Issue

**Title:** AnnData to Seurat: fix dimensions of raw layer when needed

## Description

This is to address @nh3 

When raw.X and X have different number of genes and `main_layer=['data'|'scaled_data']`, it resizes them to have the same number of genes in anndata2seurat.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0aac69ef732e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.