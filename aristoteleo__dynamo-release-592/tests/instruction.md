# Issue

**Title:** Debug arclength sampling

## Description

In pull request , the function will sample one more point when `terminate` is True and the output length is insufficient. It turns out that the check of `terminate` is not necessary. Thus, this pull request will remove it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9cc9ee4e376b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.