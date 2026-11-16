# Issue

**Title:** add patch coordinates when saving to .h5

## Description

Add the following new .h5 assets when dumping patches to h5:
- `coords`: indicates the (x, y) pixel coordinates of the top left corner for each patch (in the full resolution image, note that TENX99.tif is 0.2125um/px not 0.5um/px)
- `patch_size_src`: indicates the width/height of each patch before rescaling (hence at  0.2125um/px for TENX99)
- `patch_size_target`: indicates the width/height of each patch after rescaling (0.5um/px in our case)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2859c92ab200`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.