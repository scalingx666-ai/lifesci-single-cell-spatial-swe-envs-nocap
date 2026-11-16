# Issue

**Title:** [cpp] Improve stats calculation in row/col reorder

## Description

Motivation: The subset assignment operator results in a concatenation layer followed by a re-ordering of the rows/cols. We don't want this outer re-order layer to prevent any parallelism or other optimizations available on the inner layers, so it's time to have all the stats specialized for row/col re-ordering.

This just adds specializations for `computeMatrixStats`, `rowSums`, and `colSums` along with tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7551359f85b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.