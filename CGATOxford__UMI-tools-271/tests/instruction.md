# Issue

**Title:** added `__version__`

## Description

Having a `umi_tools.__version__` string
is the standard recommended Python way
to make the version number accessible.
This commit does that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74f6af7cf896`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.