# Issue

**Title:** Sc 51 aggregate

## Description

adds support (in `harpy.utils._aggregate`) for aggregation of:

- skewess of intensity of segmented objects
- kurtosis of intensity of segmented objects
- intensity quantiles of segmented objects
- radii and axes of segmented objects
- center of mass of segmented objects

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ff9d7404368`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.