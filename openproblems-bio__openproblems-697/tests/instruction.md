# Issue

**Title:** Run test benchmark in Tower

## Description

Moving all benchmark runs to tower. Running in GA is just too flaky.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6bbcf5c3d85e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.