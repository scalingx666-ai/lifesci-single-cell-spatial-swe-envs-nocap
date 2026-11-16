# Issue

**Title:** Move make_stitched_labels from experimental.im to experimental.tl

## Description

## What

Moves `make_stitched_labels` from `squidpy.experimental.im` to `squidpy.experimental.tl`.

## Why

The tiling-QC / cut-cell stitching workflow is four steps:

1. `tl.calculate_tiling_qc` — score cells for tile-boundary artifacts
2. `tl.assign_stitch_groups` — pair the cut pieces across seams
3. **`make_stitched_labels`** — materialise the merged labels
4. `pl.tiling_qc` — visualise

Steps 1–2 already live in `tl`, but step 3 sat in `im`. That split the pipeline across two modules and hurt discoverability. This PR co-locates the whole workflow in `tl` so users find all of it in one namespace.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a88aa7267bd7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.