# Issue

**Title:** fix: don’t crash when checking for numeric dtypes

## Description

we still crash afterwards, but with a good message

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `22eade095245`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.