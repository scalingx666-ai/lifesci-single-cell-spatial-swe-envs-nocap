# Issue

**Title:** Fix symlinks

## Description

The -L option follows symlinks and thus allows to determine the file size correctly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `93d6461d8266`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.