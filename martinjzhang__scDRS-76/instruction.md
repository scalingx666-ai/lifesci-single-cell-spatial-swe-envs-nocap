# Issue

**Title:** fixed the bug in scdrs/util.py

## Description

When mcp included NaN, significance was not displayed.
This is because multipletest()[1] is filled with NaN when p values included NaN, while multipletest()[0] is normal.
By modifying to use multipletest()[0], the problem is solved.

Related to #75

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9417105aa650`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.