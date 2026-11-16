# Issue

**Title:** feat: Add cell to specify backend device

## Description

This PR creates a specific cell to define the backend device ("cpu", "gpu" or "tpu").
It makes it clearer to the user that he needs to update the backend device if he wants to.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7f9c51b88e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.