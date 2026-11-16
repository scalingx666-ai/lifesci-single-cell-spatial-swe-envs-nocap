# Issue

**Title:** optimized getErrorCorrectMapping() with bktrees

## Description

Hi,

`umi_methods.getErrorCorrectMapping()` can be sped up drastically using a BK-Tree as data-structure for storing the whitelist of cell-barcodes. 

- the old version used pairwise comparisons to find whitelisted barcodes  1BP apart from a query.
- now we 'index' the whitelist using a BKTree, which makes retriving 1BP sequences alot faster
- depends now on the pybktree package available in pip

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60ad2786ec2a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.