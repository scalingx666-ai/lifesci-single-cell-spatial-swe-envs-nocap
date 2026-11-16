# Issue

**Title:** Storing patches embeddings as an `AnnData` object instead of images

## Description

@stergioc I made this PR to store patch embeddings inside an `AnnData` object instead of an image.

Notes:
- this `AnnData` object is linked to the GeoPandas dataframe containing the shape. So when plotting the `embeddings_patches` with `spatialdata_plot`, you can directly provide `color="cluster"` (where `cluster` is a column of `adata.obs`) and it will detect it. Or, for instance, you can use `color="0"` to show the first column value of the embeddings.
- the `AnnData` object also contains the patches locs in `adata.obsm["spatial"]`, meaning you can use [`sc.pl.spatial`](https://scanpy.readthedocs.io/en/1.10.x/api/generated/scanpy.pl.spatial.html) if you only care about the centroids of the patches (rather than their actual boundary).

Let me know if you like this!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1aa4a43f9303`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.