# Issue

**Title:** Fix normalization test in bcScore

## Description

We are now checking that data and counts are not identical. If that's the case, then for sure normalization has not happened.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2cee47af577d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.