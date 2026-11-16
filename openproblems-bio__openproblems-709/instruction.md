# Issue

**Title:** make celltype clusters tighter in celltype random embedding/graph

## Description

In immune_batch, the celltype random graph does not perform well on isolated labels F1, which is odd since it was designed for this task. The only explanation here is that louvain is combining clusters, which means the random noise is too large and thus clusters can be merged despite their clear separation. This should make the clusters tighter and thus less likely to be merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8cfae942ab0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.