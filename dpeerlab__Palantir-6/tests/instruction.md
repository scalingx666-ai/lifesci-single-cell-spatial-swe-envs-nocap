# Issue

**Title:** Fix scikit-learn dependency

## Description

As noted on the [pypi page](https://pypi.org/project/sklearn/), `scikit-learn` is the actual package.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ccbd5a4e1f09`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.