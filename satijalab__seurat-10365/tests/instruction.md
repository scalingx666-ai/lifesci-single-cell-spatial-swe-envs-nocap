# Issue

**Title:** Add warning when `FindMarkers` / `FindAllMarkers` sees an `IterableMatrix` (BPCells) w/ column-major order

## Description

(we choose to warn the user instead of forcibly transposing the storage order at once at the beginning of `FindAllMarkers`).

- Add warning in `FindMarkers`. This is only shown _once per session_.
- The warning bubbles up to `FindAllMarkers`. This is shown _every time_ `FindAllMarkers` is called (per run, not per `FindMarkers` iteration, to avoid clogging output).
- Add relevant test to `test_differential_expression.R`, skipped on CRAN.

Below is an example that demonstrates behavior with these changes.

```R
> mat_bpcells_row <- t(as(t(pbmc_small[['RNA']]$counts), "IterableMatrix"))
> mat_bpcells_col <- BPCells::transpose_storage_order(mat_bpcells_row)
> pbmc_small[['RNAbpRowMajor']] <- CreateAssay5Object(counts = mat_bpcells_row)
> pbmc_small[['RNAbpColMajor']] <- CreateAssay5Object(counts = mat_bpcells_col)
> pbmc_small <- NormalizeData(pbmc_small, assay = "RNAbpRowMajor")
# Normalizing layer: counts
> pbmc_small <- NormalizeData(pbmc_small, assay = "RNAbpColMajor")
# Normalizing layer: counts
> a <- FindMarkers(object = pbmc_small, assay = "RNAbpColMajor", ident.1 = 0, ident.2 = 1)
# Warning: Column-major order detected; FindMarkers requires row-major order.
# Consider first running BPCells::transpose_storage_order().
# This message will be shown once per session.
> b <- FindAllMarkers(object = pbmc_small, assay = "RNAbpColMajor", pseudocount.use = 1)
# Calculating cluster 0
# Warning: Column-major order detected; FindMarkers requires row-major order.
# Consider first running BPCells::transpose_storage_order() to avoid repeated transpositions.
# Calculating cluster 1
# Calculating cluster 2
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `93c686becd71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.