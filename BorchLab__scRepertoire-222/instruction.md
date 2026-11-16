# Issue

**Title:** Do not calculate bias for samples with only one cell type

## Description

Avoids a division by zero in clonalBias.R when the background frequency vector has length 1 (all expanded cells have the same cell type for a given sample). No clonal bias can be calculated when all cells have same cell type - skip these samples.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38e248ad02bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.