# Issue

**Title:** Fix inference with `fit_scaling=False`

## Description

## Bug fixes

* Prevents `scaling` to be fitted/optimized when `fit_scaling=False` is specified.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9bfd9fbfdd90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.