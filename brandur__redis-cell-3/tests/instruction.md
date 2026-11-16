# Issue

**Title:** Add `unsafe` invocations around calls on extern static

## Description

Smart of the Rust compiler to finally pick up on these (as of 1.13.0).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `127d90ab9c81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.