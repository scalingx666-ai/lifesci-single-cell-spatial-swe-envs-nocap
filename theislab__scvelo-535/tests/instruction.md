# Issue

**Title:** Move unit tests to `tests/`

## Description

## Changes

* Moves unit tests from `scvelo/core/tests/` to `tests/`
* Updates `pytest.ini` to not search `scvelo/` for tests to run

## New

* Makes `tests/` a package

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ca7e7aec59c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.