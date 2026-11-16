# Issue

**Title:** Force reload of s3 file structure on every request

## Description

This prevents from reflecting wrong structure and allows simple incorporation of newly uploaded datasets without need to restart the server

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `87a8dbfa7899`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.