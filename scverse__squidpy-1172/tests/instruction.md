# Issue

**Title:** Add derive_mpp_from_shapes utility

## Description

## Summary

Adds `squidpy.experimental.utils.derive_mpp_from_shapes`, a utility that computes microns-per-pixel of a target coordinate system from a shapes element plus one known physical measurement (spot pitch or spot diameter). Works for Visium, Visium HD bins, and any regular-grid shapes layout without relying on `scalefactors.json`.

- **Pitch path** (recommended): transforms centroids into the target CS, measures the median k=1 NN distance, returns `um_between_centers / pitch_px`. Subsamples to 5000 centroids on large grids (relevant at Visium HD bin counts).
- **Diameter path**: for Point shapes uses `2 * median(radius) * sqrt(|det A|)`; for Polygon shapes uses `sqrt(median(area) * |det A|)`, avoiding a per-geometry shapely call at HD scale.
- Anisotropic transformations are hard-rejected with a clear error and per-axis would-be mpps, since a single scalar mpp is not well-defined under non-uniform scale or shear.
- 3D shapes and `MultiPolygon` geometries are rejected with informative errors.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9aa7c09465b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.