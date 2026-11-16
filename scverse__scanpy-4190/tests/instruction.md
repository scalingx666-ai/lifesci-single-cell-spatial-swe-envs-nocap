# Issue

**Title:** ci: fix benchmarks

## Description

Looks like `setup()` only reliably runs *after* `setup_cache` if there are parameters.

So I’m returning something from `setup_cache` to introduce a “parameter”.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5a745e1258f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.