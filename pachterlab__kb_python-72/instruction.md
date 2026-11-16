# Issue

**Title:** Fix temp directory

## Description

I ran for RNA velocity and I found that the temp directory is wrong.
The default value is `'temp'`, but it doesn't include my output directory.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f80df19dc256`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.