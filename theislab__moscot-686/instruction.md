# Issue

**Title:** Set defaults of `min_iterations` and `max_iterations` to None

## Description

As discussed in  since it's hard to catch up with the changes of ottjax defaults we expose these arguments but remove them if not specified.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `389e008e5633`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.