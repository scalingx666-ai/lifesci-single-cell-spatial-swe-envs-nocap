# Issue

**Title:** [Backport release-2.2] [r] Fix build when workspace path contains spaces

## Description

Backport e21bff2a5c6a707e9c06cff41393b29c28f6361a from #4295.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c5700b8b2d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.