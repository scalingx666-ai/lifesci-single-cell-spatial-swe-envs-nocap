# Issue

**Title:** Fix for numeric stability issue

## Description

Reverting back to using init_to_mean to initialise the posterior mean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d1eab276af28`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.