# Issue

**Title:** Actions

## Description

Update GitHub actions for package checking. Currently works except for some weird behaviour on Windows.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd65a4240621`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.