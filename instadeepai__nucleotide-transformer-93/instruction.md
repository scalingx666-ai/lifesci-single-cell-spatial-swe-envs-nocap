# Issue

**Title:** fix: Fix tokenizer in SegmentEnformer and SegmentBorzoi

## Description

- Updated the tokenizer that is used for SegmentEnformer and SegmentBorzoi
- Ran the example notebooks to have the figures plotted
- Removed `shape` argument in `jnp.reshape` because it raises an error is some `jax` versions

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e53bbb1b3b97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.