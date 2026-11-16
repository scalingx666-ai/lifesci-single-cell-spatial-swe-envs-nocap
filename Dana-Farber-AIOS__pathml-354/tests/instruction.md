# Issue

**Title:** Update Environment Configuration and Dependencies

## Description

1. Excluded Python version and `python-spams` as dependencies in the `environment.yml` file.
2. Added `python-spams` dependency outside the `environment.yml` file.
3. Implemented `mamba` for environment setup.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88e806cd067d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.