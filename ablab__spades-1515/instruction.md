# Issue

**Title:** Short sequence optimization

## Description

We reuse internals of Sequence to store up to 120 bits of data (60 nucls) inlines. Effectively this means that many short k-mer sized sequences up to k=55 does not require any memory allocation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `874c54bb712c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.