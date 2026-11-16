# Issue

**Title:** Update quantile_norm to allow performing on list objects

## Description

`quantile_norm` now supports both `list` object and `liger` object. Also added random seed setting in it to allow robust reproducible results.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f1a7b98753c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.