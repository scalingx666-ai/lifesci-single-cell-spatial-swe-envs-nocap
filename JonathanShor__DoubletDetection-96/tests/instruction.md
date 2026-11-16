# Issue

**Title:** Fast(er) Normalize

## Description

Optimizes the default normalization method by memoizing the normalized `raw_counts`.

Also improves the install process robustness, and ensures consistent labeling of cells that join no cluster when `n_iters == 1`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd490f43022d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.