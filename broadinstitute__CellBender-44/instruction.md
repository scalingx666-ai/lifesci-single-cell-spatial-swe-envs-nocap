# Issue

**Title:** Return exit status 1 for input file error

## Description

If `remove-background` cannot load the input file, return exit status 1.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3482559bba4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.