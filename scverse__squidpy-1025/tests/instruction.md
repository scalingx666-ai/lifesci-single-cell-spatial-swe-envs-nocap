# Issue

**Title:** Update CI

## Description

Fixes CI by circumventing the pip issue with “resolution too deep” or trying to download some old version and failing to build it.

Also speeds up CI.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17341d062281`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.