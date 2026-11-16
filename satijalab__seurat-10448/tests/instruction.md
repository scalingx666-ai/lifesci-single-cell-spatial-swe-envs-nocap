# Issue

**Title:** Avoid densifying on-disk assays in AddModuleScore.StdAssay

## Description

This is relevant to this reported bug  

AddModuleScore.StdAssay wrapped each layer in CreateAssayObject(), which coerces the whole IterableMatrix to an in-memory dgCMatrix before scoring. For BPCells-backed v5 objects this densification dominates runtime and defeats on-disk storage, even though scoring only needs row/column reductions over a handful of gene rows.

The fix:
Extract the core scoring math into an internal .AddModuleScore() helper that operates directly on an expression matrix. AddModuleScore.Assay now delegates to it via GetAssayData(), and AddModuleScore.StdAssay runs it per layer on the raw LayerData() matrix, keeping on-disk data lazy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6981bbd71d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.