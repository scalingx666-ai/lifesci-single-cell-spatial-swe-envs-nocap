# Issue

**Title:** remove KDEpy dependency

## Description

KDEpy is not available on conda-forge and the Pypi installation is also broken for specific versions of Mac. Considering that it is only used in `pp.external.sctransform`, it would be nice to remove it from dependency.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65fd8c24dc49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.