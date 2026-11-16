# Issue

**Title:** Backport PR #4461 on branch 1.12.x (fix: avoid dtype overflow in top_segment_proportions for sparse small ints)

## Description

Backport PR #4461: fix: avoid dtype overflow in top_segment_proportions for sparse small ints

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `607339798895`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.