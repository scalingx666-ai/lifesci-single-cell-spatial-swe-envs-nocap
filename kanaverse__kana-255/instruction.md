# Issue

**Title:** Fix for incorrect type return in annotation value selection

## Description

This resolves an issue identified in the "explore" mode, where annotation values are integers (mostly found with cluster selection). However, when a user selects a specific cluster, html returns the value as a string. We implemented a type detection mechanism to infer the original type and convert the string value back to its original type.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6d0658ae005`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.