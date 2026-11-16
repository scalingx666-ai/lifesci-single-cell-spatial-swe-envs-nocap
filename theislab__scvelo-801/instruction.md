# Issue

**Title:** Refactor testing in CI

## Description

## Changes

* Adds `pytest-cov` to `requirements.txt`.
* Dependencies are now installed using `pip install -e '.[dev]'` in the `test` job.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `697c1156fe79`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.