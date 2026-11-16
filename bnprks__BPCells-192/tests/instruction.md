# Issue

**Title:** [r] fix gene score params

## Description

Params for tile width in `gene_score_width_archr()` weren't being passed down previously.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd37b9d7dbe3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.