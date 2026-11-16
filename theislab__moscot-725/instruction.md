# Issue

**Title:** Skip Regression Tests For Versions Lower Than Python 3.9 and Remove Elastic Cost

## Description

This PR fixes tests for the CI.
skipping regression tests depending on the version and removing elastic costs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3d29aee8ceb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.