# Issue

**Title:** CI improvements

## Description

- fix how dependencies are installed (faster CI)
- separate tests with cellpose v3 and v4
- specific `poe` marks for every combination of interest
- fix caching

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4bb0b71d217c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.