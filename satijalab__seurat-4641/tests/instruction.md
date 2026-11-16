# Issue

**Title:** Allow user to specify images to Load10X_Spatial

## Description

- `Load10X_Spatial()` add a new parameter `image` to allow user to pass in an image.
- `Read10X_Image()` adds a new parameter `image.name` to allow user to specify a custom image other than _tissue_lowres_image.png_.
- Practically the idea is to allow user to read in high resolution slide image if needed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d67d73e12b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.