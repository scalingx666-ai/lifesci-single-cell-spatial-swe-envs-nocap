# Issue

**Title:** Clean up kernels Templates

## Description

Cleaning up dtype dispatching and functions. Switched out /sqrt for the more performant *rsqrt. Confirmed no speed regression vs old implementation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d92126d7afd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.