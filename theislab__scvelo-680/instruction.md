# Issue

**Title:** Update Python versions in CI

## Description

## Changes

* Runs linting job in Python 3.8.
* Runs unit tests in 3.9 as well.

## Related issues

Related to #545.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5407fc3e5985`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.