# Issue

**Title:** more flexible loading method

## Description

Problem addressed: the reducer and index paths may diverge when using experiment tracking software that automatically assigns names to uploaded artifacts.
The `load` method should be flexible enough to take in as arguments the two paths required to load the reducer.

This change maintains backwards-compatibility with `common_prefix` as the only argument.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01f0a212cb48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.