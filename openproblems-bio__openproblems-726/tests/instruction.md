# Issue

**Title:** separate bedtools from everything else

## Description

bedtools takes a long time to install. Putting it in a separate image.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `271c7ff2ac11`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.