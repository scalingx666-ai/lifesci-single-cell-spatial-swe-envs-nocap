# Issue

**Title:** Fix conversion wide-to-long format

## Description

Fixes issue #160. Also adjusts `.cntEval` function to ignore `NA` values when computing rowSums of expression matrix.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e99b49e00be5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.