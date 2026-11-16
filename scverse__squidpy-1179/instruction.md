# Issue

**Title:** chore: add flaky marker to pyproject

## Description

similar to the gpu marker we needed to add even though the CI's worked here:  We need to add the flaky marker explicitly here.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `093217db7d24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.