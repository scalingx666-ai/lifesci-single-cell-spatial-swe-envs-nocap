# Issue

**Title:** v1.3 Voting Classification

## Description

A cell is called 'doublet' when the cell's p-value exceeds parameter `p-thresh` (default 0.99) on at least `voter_thresh` (default 90%) of the runs (when `n_iters` > 1).

Also handles cells assigned to -1 "not a cluster" cluster by Phenograph: they are excluded from score and p-value calculations. Raises a warning if a cell is assigned -1 on all runs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9f7788b9b94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.