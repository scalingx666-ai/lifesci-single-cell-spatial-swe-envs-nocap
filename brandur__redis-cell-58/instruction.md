# Issue

**Title:** Ceil fractional retry_after and reset_after

## Description

I have faced 429s several times after waiting what the retry headers say. They are filled with `num_seconds()`, which obviates the fractional part of the duration.

This patch ceils the value if there is a fractional part (in milliseconds).

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e339d512c8be`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.