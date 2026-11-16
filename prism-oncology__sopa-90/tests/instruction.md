# Issue

**Title:** Improvements for Cellpose segmentation

## Description

Made the following changes:

- Cellpose weights are now correctly used, previously Cyto3 was always applied instead
- Added an optional parameter clahe_kernel_size for skimage.exposure.equalize_adapthist which can be relevant for very big cells or patches. The default still is 1/8 of patch width and height
- Blur and CLAHE can be disabled by setting the parameter to 0
- If segmentation is run on multiple channels (e.g Nucleus marker + cell boundary marker) blur and CLAHE are now run on every channel separately which prevents spillover of intensities

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0756ac53e02e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.