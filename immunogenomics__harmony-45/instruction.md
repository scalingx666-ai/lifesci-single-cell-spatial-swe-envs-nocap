# Issue

**Title:** Add option for reduction and project.dim to RunHarmony.Seurat

## Description

Hi, I added a couple of options to `RunHarmony.Seurat` here to make it a bit more flexible with other data types (especially for scATAC-seq). Added the `reduction` argument to allow running on reductions other than PCA, and the `project.dim` argument to change whether the projection is run after running harmony.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `818123eff65e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.