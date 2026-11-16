# Issue

**Title:** Fix the `__version__` deprecated warning

## Description

hi

without this usage of `anndata.__version__` would cause a warning

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `761a3c844114`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.