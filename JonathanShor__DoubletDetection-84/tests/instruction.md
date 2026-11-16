# Issue

**Title:** Set phenograph parameter 'prune'=True by default.

## Description

User must specifically pass 'prune': False in phenograph_parameters to change this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3bc065e77b80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.