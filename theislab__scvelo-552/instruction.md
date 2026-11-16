# Issue

**Title:** Refactor `cleanup`

## Description

## Changes

* Renames arguments of `cleanup`. `data` is superseded by `adata`, `copy` by `inplace`.
* Variable names in `cleanup` are updated to be more informative.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2a7e84673ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.