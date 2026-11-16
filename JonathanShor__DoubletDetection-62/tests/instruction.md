# Issue

**Title:** Voting scheme

## Description

Updates classification methodology: cells with p-value > 0.99 on at least 90% of iterations are called doublets. Both thresholds are parameters to `.fit` (these are the default values).

Updates `n_iters`, `n_top_var_genes`, and `phenograph_parameters` defaults to be in line with updated methodology.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ebb2c5dcf2cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.