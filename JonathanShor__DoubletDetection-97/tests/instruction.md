# Issue

**Title:** Fix masked labels filling for ambiguous cells

## Description

Current filling accidentally assigned a true value to cells that were never clustered. This properly assigns these cells a np.nan label

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9281a099703b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.