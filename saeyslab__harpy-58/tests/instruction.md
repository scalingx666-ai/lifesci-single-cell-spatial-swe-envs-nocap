# Issue

**Title:** Sc 28 rasterize

## Description

- change name of `sp.im.add_labels_layer_from_shapes_layer` to `sp.im.rasterize`.
- use datashader for rasterizing shapes layer to labels layer insteas of rasterio. TODO: remove rasterio depedency from the shapes manager and baysor implementation. 
- do custom scaling using dask, because passing dask geopandas to datashader does not result in desired increase in performance. Also implementation of spatialdata is too slow and uses too much memory to rasterize e.g. Merscope segmentation shapes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61052baa6419`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.