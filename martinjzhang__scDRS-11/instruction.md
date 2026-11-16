# Issue

**Title:** Unit test

## Description

1. Added unit tests for subroutines _select_ctrl_geneset, _compute_raw_score, _compute_overdispersion_score, _correct_background
2. Added test for compute_stats in the implicit covariate correction mode

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dc933a89889b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.