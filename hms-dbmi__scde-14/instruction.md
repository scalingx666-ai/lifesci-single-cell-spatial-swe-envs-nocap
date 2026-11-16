# Issue

**Title:** Pass verbose argument to calculate.crossfit.models

## Description

`scde.error.models` function should propagate verbosity to other functions such as `calculate.crossfit.models`. Actually for the readability purposes, it would be better to split arguments into multiple lines and to align them.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `932053ac9169`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.