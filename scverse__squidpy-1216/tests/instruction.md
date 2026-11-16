# Issue

**Title:** [3/3] cp_measure features + coordinate alignment for calculate_image_features

## Description

Final piece of #982 (split from #1189, #1190). Adds cp_measure features and image/labels coordinate alignment.

### New deps (hard)
`cp-measure>=0.1.19,<0.2`, `centrosome>=1.2.3`.

### Usage
```python
sq.experimental.im.calculate_image_features(
    sdata, image_key="img", labels_key="cells",
    features=["cpmeasure:sizeshape", "skimage:morphology", "squidpy:summary"],
)
```
- `features=None` -> all features, all backends (needs an image).
- `align_mode="strict"` (default) raises on non-pixel-aligned image/labels; `"rasterize"` resamples onto the image grid.

### Notes
- Boundary cells outside the image/labels overlap are dropped + reported.
- Multiscale labels: alignment works for identity/integer-translation; `rasterize` raises (pre-align instead).
- cp_measure columns keep raw CellProfiler names.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `005c9056fea7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.