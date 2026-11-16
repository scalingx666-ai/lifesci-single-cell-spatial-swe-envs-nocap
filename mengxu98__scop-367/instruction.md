# Issue

**Title:** feat: add SpatialDM spatial communication backend

## Description

## Summary

- add `RunSpatialDM()` with official global and local SpatialDM statistics
- run a pinned SpatialDM 0.3.1 backend in a standalone Python 3.10 subprocess environment
- add `GetSpatialDMResult()` and SCOP-style weight, global, and local plots
- register SpatialDM with `RunCCC()` without forcing `group.by` or fabricating sender-receiver edges
- document the workflow and add spatial/backend regression tests

## Why

SpatialDM fills the spatial ligand-receptor association gap between group-level communication methods and directional transport methods. Its bivariate Moran statistics identify spatially associated LR pairs and local interaction spots, but they are not cell-type sender-receiver edges. The integration therefore stores SpatialDM as a non-edge association result and keeps Moran's R semantics explicit.

## Implementation notes

- raw analysis coordinates use the existing strict `SpatialCoordinates()` contract
- normalized/log-transformed expression is passed through `AnnData.X`; raw counts are retained in `AnnData.raw` for the official local workflow
- human/mouse built-in CellChatDB and custom LR tables are supported
- weight matrices, effective ranges, cell/feature identities, source coordinates, parameters, backend versions, and the pinned Git SHA are stored in a schema-v1 bundle
- `SpatialDMPlot()` returns SCOP `ggplot`/`patchwork` objects for weight diagnostics, global Moran results, and local LR maps

## Validation

- `test-run-spatialdm.R`: 28 passed
- `test-run-commot.R`: 54 passed
- `test-run-spatalk.R`: 108 passed
- real pinned SpatialDM subprocess smoke: passed (`REAL_SPATIALDM_OK`), including global/local output and all three plot types
- `pkgload::load_all('.', quiet = TRUE, compile = FALSE)`: passed
- Python runner compilation and `git diff --check`: passed
- full `rcmdcheck` source build/install completed; the local Windows check retained the existing DESCRIPTION/locale metadata failure and did not introduce dependency-in-code or unstated-example dependency warnings

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `addc66f309cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.