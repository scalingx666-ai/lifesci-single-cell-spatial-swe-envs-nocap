# Issue

**Title:** Debug `is_normalized()` in Markov

## Description

Bug description: `not P` checks either `True/False` or `None`, which will raise a bug under some circumstances. `P is None` is the better way to perform the check.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e87f702da0eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.