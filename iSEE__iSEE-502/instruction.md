# Issue

**Title:** Enable custom saving of the application state.

## Description

This allows enterprise deployments to persist the application state, in a manner very similar to Shiny's bookmarking feature but somewhat more flexible with respect to allowing the user to choose where the files ultimately live.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60106738a423`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.