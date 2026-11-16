# Issue

**Title:** Validate the selection sources to avoid app crash, fix #457.

## Description

Factored out utilities for choosing selection sources.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1975f39e1b44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.