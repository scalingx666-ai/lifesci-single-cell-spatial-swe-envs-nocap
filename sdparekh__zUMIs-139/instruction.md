# Issue

**Title:** Ensure that at least 1GB of RAM is available for each samtools sort call.

## Description

This catches the case where 0 GB would be available to samtools if no memory limit was specified and the user allowed to use over 100 threads.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b35f4c68b783`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.