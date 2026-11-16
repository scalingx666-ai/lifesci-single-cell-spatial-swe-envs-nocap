# Issue

**Title:** Update vignette for Seurat v4

## Description

Seurat v4 changes the names of the markers table
The logFC column is now called avg_log2FC
This change updates the vignette to support the new name

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2cdc01016c54`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.