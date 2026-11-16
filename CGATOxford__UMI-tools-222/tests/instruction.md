# Issue

**Title:** refactoring writing out count data to reduce memory req.

## Description

@romanhaa is getting an error due to the memory requirements to pivot a dataframe in `pandas` (#219). Use of `pandas` is overkill here so I've refactored to just use a simple `dict`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b75a2aa9331b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.