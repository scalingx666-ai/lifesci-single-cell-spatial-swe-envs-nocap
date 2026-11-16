# Issue

**Title:** Fix `optimization.py::get_weight`

## Description

## Bugfixes

* Fixes case where `perc` is numeric but not an integer which previously caused the `else` instead of `if` clause to be entered.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b9893ed4c1d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.