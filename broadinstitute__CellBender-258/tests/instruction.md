# Issue

**Title:** Move hash computation so that it is recomputed on retry, and now-inva…

## Description

…lid checkpoint is not loaded.

If number of tries is exhausted, and ELBO tests are still failing, allow to complete anyway (using checkpoint) so that outputs are produced, but exit(1).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `02dd763fdb3b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.