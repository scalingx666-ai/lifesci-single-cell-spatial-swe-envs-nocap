# Issue

**Title:** [python] Fix, catch, or ignore many of the warnings in pytest

## Description

The primary change in this PR is updating tests that used deprecated `None` values in `shape` or `domain`. The tests were either updated to specify shape/domain or used with pytest `deprecated_call`. In addition, warnings that contain "this looks like a string-form forward reference imported from another module" are now ignore by pytest (these are just warnings about skipping type checking).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d7f3bb80bb11`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.