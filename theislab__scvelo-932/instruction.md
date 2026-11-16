# Issue

**Title:** Fix deprecation of keyword argument `copy`

## Description

## New

* Add `core/_utils.py` with wrapper `deprecated_arg_names`.

## Changes

* Use local wrapper `deprecated_arg_names` instead of Scanpy version.

## Related issues
.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc1e200d572b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.