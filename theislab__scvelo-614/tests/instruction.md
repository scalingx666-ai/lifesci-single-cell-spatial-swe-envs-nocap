# Issue

**Title:** Catch error in steady state calculation

## Description

## Changes

* Catch non-positive parameter values and raise `ValueError`

## New

* Add unit test `TestSplicingDynamics.test_steady_state_not_defined` to raising of `ValueError`.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06734980fae6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.