# Issue

**Title:** Enable using a `scale>0` in staining-based segmentation

## Description

Currently, staining-based segmentation always operates at `scale0` (highest resolution), which is recommended for better performance.

Yet, when the segmentation is used as a prior (e.g., for proseg), it can be computed at a larger scale (lower resolution) to speed up the prior segmentation. It would lead to slightly lower segmentation, but it may be corrected in the second round of segmentation.

To use it, simply provide the scale in `sopa.make_image_patches`:
```python
sopa.make_image_patches(sdata, scale="scale1", ...)
```

⚠️ Currently, this feature is only supported via the API. CLI/pipeline support will be added in a future PR (please comment in  if this is of interest to you).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f3c07608fde`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.