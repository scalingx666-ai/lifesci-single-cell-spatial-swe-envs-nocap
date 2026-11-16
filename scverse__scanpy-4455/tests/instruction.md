# Issue

**Title:** ci: reduce memory use

## Description

to fix the hatch-test.stable job from crashing all the time.

circumvents  for the worst case

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f523e64ebb3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.