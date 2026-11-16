# Issue

**Title:** Add spatial coordinates to Anndata when converting from SpatialExperiment

## Description

The aim is to add the spatial coordinates to `adata.obsm["spatial"]` when converting SpatialExperiment objects via `zellkonverter::writeH5AD`. Please see [this issue]( ) for more context.

@lazappi, you mentioned moving this to the R side and leaving the conversion code, so I've done this by adding the coordinates to `reducedDims` as a workaround.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41861c688218`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.