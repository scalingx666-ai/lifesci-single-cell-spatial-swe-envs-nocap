# Issue

**Title:** Transfer all buffers when posting TypedArrays to the main thread.

## Description

This should eliminate any latency due to message transfer between workers.

However, it requires a lot more discipline with respect to understanding the memory store of the arrays being posted.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c47fd7d680e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.