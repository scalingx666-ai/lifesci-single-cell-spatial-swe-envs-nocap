# Issue

**Title:** Enabling tests and docs against pre-released spatialdata

## Description

Useful to test the build before making a release.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4070a61e5480`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.