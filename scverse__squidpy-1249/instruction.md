# Issue

**Title:** fix: ensure radius values stored in AnnData.uns are writable

## Description

`RadiusBuilder` and `DelaunayBuilder` stored an interval `radius` in
`adata.uns['spatial_neighbors']['params']` as the tuple it was passed as.
`anndata` has no I/O spec for tuples, so any object built with a tuple `radius`
raised `IORegistryError` on `write_h5ad` / `write_zarr`.

Store a list instead, via a small `_radius_to_uns` helper. Scalar radii are
unchanged. Note that `DelaunayBuilder` already normalizes a scalar `r` to
`(0.0, r)` in `__init__`, so `spatial_neighbors_delaunay(radius=5.0)` now records
`[0.0, 5.0]` — the same value as before, just writable.

The abstract `GraphBuilder.uns_params` docstring now states that values must be
writable by `anndata`, so custom builders don't reintroduce the same problem.

Regression test covers both builders with scalar and interval radii, and asserts
on an actual `write_h5ad` rather than only on the stored value.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8dff5dead89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.