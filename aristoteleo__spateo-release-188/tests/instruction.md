# Issue

**Title:** Remove non-conda-forge package from requirement

## Description

Remove packages that are not available in conda-forge to ensure compatibility with the conda-forge channel. Users will then need to install those packages separately to fulfill their dependencies.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6bd4e7f68757`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.