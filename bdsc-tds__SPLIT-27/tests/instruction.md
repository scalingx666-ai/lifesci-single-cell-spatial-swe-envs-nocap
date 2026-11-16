# Issue

**Title:** feat: remove residual contamination from genes not supported by deconvolution model

## Description

## Summary

Adds an optional residual contamination removal step to `purify()` via the new
`DO_remove_residual_contamination = TRUE` flag (off by default, fully backward compatible).

## Problem

Standard SPLIT purifies profiles by proportionally redistributing signal between
assigned cell types. However, genes that are not specific to any of the assigned
cell types — contamination from cell types entirely absent from the local
deconvolution model — cannot be resolved by proportional redistribution and
persist in the purified profile.

## Solution

When `DO_remove_residual_contamination = TRUE`, genes with no reference support
in any of the assigned cell types are zeroed out explicitly. The specificity
threshold is automatically derived from the reference distribution (75th percentile
of the min/max expression ratio across genes), requiring no manual tuning.

On a public Xenium breast cancer dataset, this removes an additional ~2–5% of
counts on top of standard SPLIT, with a measurable improvement in marker gene
specificity across cell types.

## Changes

- `R/method_agnostic_purification.R`: add `DO_remove_residual_contamination` and
  `belonging_threshold` arguments to `rctd_free_purify()` and `purify()`; remove
  `epsilon` from the purification formula (orphan genes now explicitly zeroed)
- `NEWS.md`: add v0.3.0 section
- `README.md`: update quick start and what's new
- `vignettes/Residual_Contamination_Removal.Rmd`: new focused vignette
- `vignettes/Run_RCTD_and_SPLIT_on_Xenium.Rmd`: add note on agnostic interface
  and py-RCTD

## Testing

Validated on Xenium NSCLC breast cancer data (Janesick 2023) and ABC Atlas
MERFISH whole-brain section 38. DotPlot and specificity score comparisons
included in the new vignette.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f226987f0fec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.