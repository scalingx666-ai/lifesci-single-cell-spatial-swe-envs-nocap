# Issue

**Title:** Fixes CPU warning bounds

## Description

Stops trim_galore from warning about using more than 8 cores when using exactly 8 cores.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55fc0ce41257`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.