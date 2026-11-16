# Issue

**Title:** Debug `vf.hessian()`

## Description

Bug description: When the `effector` is not provided, an error will be raised because `list` object doesn't have the method `to_list()`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e87f702da0eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.