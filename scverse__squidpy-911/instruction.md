# Issue

**Title:** Update spatialdata dependency

## Description

## Description

The latest version of xarray directly includes `DataTree` but with a datamodel that is different from before. Since the xarray version was not constraint in `SpatialData` this led to errors. The current latest version of `SpatialData` constraints the xarray version used until the latest version of xarray is supported.

## How has this been tested?

local tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7750b01b6bc3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.