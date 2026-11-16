# Issue

**Title:** Bugfix/cell neighborhood rank tokenizer

## Description

Updates to `cell_neighborhood_rank_tokenizer.py`:
- copies changes related to `separate_cell_and_neighborhood_tokens` that were published in `jepa` branch, but not yet merged into `main`.
- adds docstring for `separate_cell_and_neighborhood_tokens`
- adds comment for clarifying `norm_factor` (non) usage in `analytic_pearson_residuals`
- renames `normalize_by_nonzero_medians` to `normalize_by_nonzero_means` because the tokeniser notebook in the nichejepa-reproducibility loads a file containing mean values not median values.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ce9fbe95c92`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.