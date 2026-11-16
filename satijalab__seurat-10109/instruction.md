# Issue

**Title:** Update `Load10X_Spatial` with new parameters

## Description

These updates are intended to allow users to be able to simplify data loading when needing options beyond what is currently available in this function.

- Add `image.name` parameter that exposes `image.name` in `Read10X_Image` and `Read10X_Segmentations`. 
  - Designed specifically to allow users to load `tissue_hires_image.png` instead of the default `tissue_lowres_image.png`. 
  - Also loads proper scale factor for plotting, based on image scale factor.
  - With these changes, coordinate scaling & transformation for segmented outputs has been moved from the loading functions to plotting functions.
- Add `segmentation.type` parameter that exposes `segmentation.type` in `Read10X_Segmentations` and `Load_10X_HD_GeoJson`.
  - Allows users to choose whether to load cell or nucleus segmentations, with cell segmentations loaded by default.
  - Only considered when `"polygons"` option is specified in `bin.size`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `175ff006cd5e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.