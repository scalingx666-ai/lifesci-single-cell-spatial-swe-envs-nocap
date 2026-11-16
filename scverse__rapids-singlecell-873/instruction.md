# Issue

**Title:** Add min_cells to Mixscape instead of reusing min_de_genes

## Description

Mirrors scverse/pertpy#1189.
`Mixscape.mixscape` gets a `min_cells` parameter for the minimum number of cells that must stay classified as perturbed, which `min_de_genes` silently controlled before, matching pertpy and Seurat's fix in satijalab/seurat#10299.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90ccd3becb59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.