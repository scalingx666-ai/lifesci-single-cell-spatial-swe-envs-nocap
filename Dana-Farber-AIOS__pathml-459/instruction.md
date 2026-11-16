# Issue

**Title:** Updating TQDM dependency and packages for testing.

## Description

- Adjusting the TQDM dependency.
- Updated all test YAML and environment YAML files.
- Pin specific versions of coverage and numba to ensure smooth testing on Python 3.10. 
- Updated how the tests access the publication page to avoid security error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `002653cec2c3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.