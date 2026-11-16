# Issue

**Title:** Fixes/cli and points

## Description

Fixes:
- CLI was broken. Fixed and added tests.
- Using points instead of shapes for visualizing circles, otherwise performance is bad.
- Removed gray border when showing points.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bde28218041f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.