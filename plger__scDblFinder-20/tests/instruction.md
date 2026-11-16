# Issue

**Title:** Fixed computeDoubletDensity.

## Description

Got rid of the squaring to make it not so bad. Also slightly faster, has less code, and got rid of a CHECK warning.

Also, threw in a GitHub Action to perform `R CMD check` for incoming commits.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a93e2c3c399`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.