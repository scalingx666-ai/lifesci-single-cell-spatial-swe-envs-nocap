# Issue

**Title:** fix bug on str to int on -k is float

## Description

Need to change `int` to `float` function. Because when k=0.6 is passed in, you will get this error: `ValueError: invalid literal for int() with base 10: '0.6'`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `62b3b3818625`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.