# Issue

**Title:** Update `run_magic_imputation` to make setting small values to 0 optional

## Description

These changes keep the default behavior of `run_magic_imputation` the same while allowing users to select if the matrix will be made sparse and the threshold that will be used to set small values to zero.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2e79472f6e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.