# Issue

**Title:** remove lock file

## Description

this file is only so multiple devs can get the same env, but this isn't really necessary for how we are doing things.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5bfcca796934`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.