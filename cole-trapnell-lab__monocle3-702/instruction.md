# Issue

**Title:** New plotting functions for QC steps in data processing

## Description

I wrote some new functions for data processing QC. They currently live in the zscape pipeline but should be migrated here.
- `plot_umi_per_cell`
- `plot_mito_umi_per_cell`
- `plot_umi_per_cell_and_perturbation`
- `plot_cells_per_sample_and_perturbation`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `735bc900527a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.