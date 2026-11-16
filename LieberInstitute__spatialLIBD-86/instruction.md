# Issue

**Title:** Registration wrapper k2

## Description

Currently using a registration variable with two groups causes `registration_wrapper()` to error out, as `registration_stats_anova` fails with k=2. To solve this, when k=2 the function now throws a warning and only returns stats from the enrichment test, anova and pairwise are NULL.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c82c789d8538`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.