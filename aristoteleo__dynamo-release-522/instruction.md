# Issue

**Title:** Replace recipe_monocle into Preprocessor for the recipes in tools

## Description

1. Replace recipe_monocle into Preprocessor for the recipes in tools.
2. convert_gene_name should be called first than basic_stats, due to it has the inplace option for valid genes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c9123ee577a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.