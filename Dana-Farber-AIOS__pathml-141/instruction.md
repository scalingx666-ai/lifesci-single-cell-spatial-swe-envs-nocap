# Issue

**Title:** Prepare package for pypi and conda

## Description

Rewrite setup.py and README. When java dependencies are called but not installed, prompt user to install.

Update environment.yml with latest dependencies.

With these changes pathml is installable from pypi and conda.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16d3d7ffa979`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.