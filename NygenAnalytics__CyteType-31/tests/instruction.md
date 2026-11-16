# Issue

**Title:** Update API URL, add natsort, and bump version to 0.6.0

## Description

Updated the CyteType API URL in both the README and config.py to reflect the new endpoint. Added natsort as a dependency and used it for natural sorting of cluster labels in main.py. Updated dependencies in pyproject.toml to use compatible version specifiers and bumped the package version to 0.6.0.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9dd68ff3bbf0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.