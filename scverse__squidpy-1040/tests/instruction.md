# Issue

**Title:** zarr v3 support

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description

- removes `<3.0.0` constraint for the Zarr package (required for the incoming `spatialdata` release)
- replaces a method that was deprecated in `spatialdata` and that will be removed in the incoming release

## How has this been tested?

Subset of tests run locally (waiting for the CI tests to emit the status).

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `662165070dcc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.