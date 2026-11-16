# Issue

**Title:** fix: read images and scalefactors from adata.uns[spatial_key]

## Description

## Description

`spatial_scatter` checked the image keys under `adata.uns[spatial_key]` but loaded images and scalefactors from `adata.uns["spatial"]`, so any other `spatial_key` failed. This loads images, scalefactors and segmentation images from `adata.uns[spatial_key]`, as the `library_id` docs describe.

## How has this been tested?

Added a test that puts different images and scalefactors under `uns["spatial"]` and `uns["spatial_trans"]` and checks that the ones under `spatial_key` are used. It fails on main. Also checked `spatial_scatter` on the Visium H&E crop with `spatial_key="spatial_trans"`, and the existing plotting tests pass.

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `493f3ddcba0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.