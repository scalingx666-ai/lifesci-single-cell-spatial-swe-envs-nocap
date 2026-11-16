# Issue

**Title:** Remove custom t-SNE implementation

## Description

No need to have it, already include multicore-tsne and many other fast t-SNEs exist.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fdd1232c0fb9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.