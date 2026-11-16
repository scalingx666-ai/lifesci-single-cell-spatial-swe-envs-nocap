# Issue

**Title:** Update docs

## Description

Update README and move instructions for setting up local environment to CONTRIBUTING.rst
Update contributor instructions in CONTRIBUTING.rst
Fix some broken docstrings
Add warnings in docstring of SegmentMIF to indicate external dependency on deepcell and incompatibility with dask distributed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9443765122a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.