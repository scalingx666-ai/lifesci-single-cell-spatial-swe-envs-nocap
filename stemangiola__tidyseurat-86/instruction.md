# Issue

**Title:** Use rlang instead of ellipsis for dot checking

## Description

Since ellipsis is superseded / deprecated in favour of rlang 1.0 https://rlang.r-lib.org/news/index.html#argument-intake-1-0-0

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82b6aec56179`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.