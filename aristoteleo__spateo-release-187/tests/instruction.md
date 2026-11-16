# Issue

**Title:** Copy logging-release code

## Description

copy the logging-release code to external and remove logging-release from requirements

PS: CI workflow is updated to pass the check. The older version raises a cache error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7572bb6189fe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.