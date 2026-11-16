# Issue

**Title:** Upload coverage in a single job

## Description

Coverage upload is flaky. This separates the flake from the real testing, and only does it once.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b065ac136941`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.