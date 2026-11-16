# Issue

**Title:** Removing duplicate barcodes

## Description

combineContigs function now also removes duplicate barcodes which appear when 1 cell has both alpha and beta TCR chains (or heavy and light BCR).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81d66b6b50d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.