# Issue

**Title:** Run builds in parallel

## Description

Docker has variable cpu utilisation due to disk and network constraints. This increases parallelism.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6c889ba16df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.