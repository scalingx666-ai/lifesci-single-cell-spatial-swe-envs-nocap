# Issue

**Title:** Change assay.use to default to DefaultAssay() instead of "RNA"

## Description

Given the tools provided by the Satija lab where a Seurat object has a built in default, I have always thought it perplexing why Harmony always defaults to RNA. Here I changed the required lines (81 and 84) and it seems RStudio removed many spaces. I think this change makes the method for Seurat objects fit better in the existing structure of Seurat.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8f4901ef92d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.