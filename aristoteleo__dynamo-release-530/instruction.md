# Issue

**Title:** Debug inverse norm

## Description

Fixed two bug in the inverse_norm caused by previous modification on `.uns["pp"]["norm_method"]`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58acb635f399`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.