# Issue

**Title:** Speed up CI

## Description

## Changes

* Ignore `tests/datasets/test_datasets.py` in `test` job of CI.
* Add job `test-dataset-downloads` to CI which only runs on `ubuntu-latest` and Python 3.8.
* Skip `test_datasets.py:TestDataSets` if Python version is not 3.8 and OS not Linux.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4add9a29e38f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.