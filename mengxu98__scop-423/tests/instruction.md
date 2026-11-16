# Issue

**Title:** fix: keep velocity matrices stored as assay layers

## Description

## Problem

A user report showed `RunSCVELO()` failing right after the Seurat to AnnData conversion:

```
Error in `py_call_impl()`:
! log_message.LogMessageError: Error in scVelo analysis: 'Ms'
```

`Ms` is an internal scVelo matrix, so the message points at nothing the user controls. Two things were wrong behind it:

1. `srt_to_adata()` matched `assay_y` only against the **assays** of the object. Velocity matrices kept as extra **layers** of the `RNA` assay (Seurat v5: `as.Seurat()` on a velocity h5ad, or `srt[["RNA"]]$spliced <- ...`) were dropped without a message. Separate `spliced`/`unspliced` assays worked, which is why the documented examples never caught it.
2. scVelo does not raise when `spliced`/`unspliced` are missing: `scv.pp.moments()` logs "Skipping moments, because un/spliced counts were not found." and returns, and the first `adata.layers["Ms"]` lookup fails afterwards.

## Changes

* `srt_to_adata()` resolves each `assay_y` name against the assays first, then against the layers of `assay_x` (new helper `get_adata_sparse_layer()`). Names that match neither are reported together with the available assays and layers. Applies to `srt_to_h5ad()` as well, which shares the conversion.
* The scVelo workflow reports the missing layers with the available ones instead of raising `KeyError('Ms')`, and computes the moments itself when scVelo skips them.
* `assay_y`/`layer_y` documentation, a velocity note in the vignette, and a NEWS entry.
* New regression test `tests/testthat/test-data-convert-velocity-layers.R`: both storage layouts produce the layers with the expected values, and unresolved names warn. It fails 5/6 assertions without the fix and passes 6/6 with it.

## Verification

* Reproduced the exact user error before the change (`Skipping moments` + `Error in scVelo analysis: 'Ms'`) and confirmed both layouts now run scVelo end to end, including `return_seurat = TRUE` (`stochastic_umap`, velocity metadata, `tools$SCVELO`) and `srt_to_h5ad()` writing both layers.
* Conversion- and Python-related test subsets: 510 + 308 assertions pass, no failures (pre-existing warnings/skips only).

The second commit only syncs `man/RunDoubletCalling.Rd`, whose documented default went stale when the data object was renamed to `object` in #421.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c486c263621f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.