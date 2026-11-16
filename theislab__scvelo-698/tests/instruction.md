# Issue

**Title:** Fix and unit test `get_mean_var`

## Description

## Bug fixes

* Makes `get_mean_var` work with sparse input and `ignore_zeros=True`.
* Update `get_mean_var` to use same size parameter for mean and variance.
* Fix `get_mean_var` s.t. passing `perc` works.

## New

* Adds `TestGetMeanVar` to unit test `get_mean_var`.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e986468496bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.