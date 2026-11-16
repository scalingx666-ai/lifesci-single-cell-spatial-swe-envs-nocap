# Issue

**Title:** Pass contents to .singleSelectionValue instead of pObjects.

## Description

Avoid potential privilege escalation from unnecessary write access.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `825432e37b9d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.