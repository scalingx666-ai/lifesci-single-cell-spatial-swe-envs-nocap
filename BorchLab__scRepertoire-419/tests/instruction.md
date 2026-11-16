# Issue

**Title:** Update loadContigs.R

## Description

Prevent file.pattern from being NULL, causing all files in the directory to be read.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9d8f6d95796`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.