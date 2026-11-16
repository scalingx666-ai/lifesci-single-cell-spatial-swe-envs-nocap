# Issue

**Title:** [2/3] Add assign_stitch_groups (tile-cut stitching algorithm)

## Description

## What

Second PR of the 3-way split of #1170. Adds `sq.experimental.tl.assign_stitch_groups` (+ `StitchParams`): given the `is_outlier=True` cells flagged by `calculate_tiling_qc` (PR-A, #1188), it pairs facing cut edges across tile boundaries, scores each candidate pair, and assembles high-confidence pairs into stitch groups via union-find.

It **only annotates** `.obs` (four columns) plus a `.uns["tiling_stitch"]` audit block; the labels element is **never modified**. Materialising a stitched labels element is PR-C (`make_stitched_labels`, follows this one).

```python
sq.experimental.tl.calculate_tiling_qc(sdata, "labels")      # PR-A (merged)
sq.experimental.tl.assign_stitch_groups(sdata, "labels")     # this PR
# sq.experimental.im.make_stitched_labels(sdata, "labels")   # PR-C (next)
```

## The score: a transparent flat mean, not a fitted model

@selmanozleyen asked to review the math/intuition of `stitch_confidence` and whether it is a novel/fitted formula. Short answer: **it is not fitted.** An earlier prototype on this branch (`ba60119f`) shipped an L2-regularised logistic regression with coefficients fit on 2197 synthetic disk pairs. We **removed it deliberately** — fixture-fit weights claim a calibration they cannot honour on real data, and squidpy should not silently encode a synthetic distribution. The score is now the **flat (unweighted) mean of five standard, bounded geometric descriptors**, each in `[0, 1]`. The features are recorded in `.uns["tiling_stitch"]`.

For a facing cut-edge pair (each a 1-D chord `extent=(lo, hi)` at perpendicular `coord`):

1. **`iou`** — 1-D extent IoU of the two chords: `overlap / (len_a + len_b - overlap)`. Do the two cut faces line up laterally?
2. **`endpoint_match`** — `max(0, 1 - (|a_lo-b_lo| + |a_hi-b_hi|) / max(len_a, len_b))`. Do the faces start/end at the same lateral positions?
3. **`merge_compactness`** — `min(4*pi*A / P^2, 1)` of the closed union mask's largest component. A re-joined real cell is compact; a false merge is elongated. Strongest single discriminator.
4. **`merge_solidity`** — `area / convex_hull_area` of the same component (clamped to 1). A false merge creates a concave waist at the join.
5. **`gap_proximity`** — `clip(1 - gap / (2*close_radius), 0, 1)`. The seam gap relative to the **closing reach** (the scale at which morphological closing could actually bridge it) — independent of the `max_gap` search radius; neutral (`1.0`) when closing is disabled.

`stitch_confidence(pair) = mean(the five features)`. Per-cell group confidence is the `min` over the group's pairwise confidences (weakest link).

### Runnable MREs (pure numpy/scipy/skimage, no squidpy)

The 1-D edge features:

```python
def extent_iou(a, b):
    o = max(0.0, min(a[1], b[1]) - max(a[0], b[0]))
    u = (a[1] - a[0]) + (b[1] - b[0]) - o
    return o / u if u > 0 else 0.0

def endpoint_match(a, b):
    d = abs(a[0] - b[0]) + abs(a[1] - b[1]); m = max(a[1] - a[0], b[1] - b[0])
    return max(0.0, 1.0 - d / m) if m > 0 else 0.0

# true cut: two faces span the same range          false pair: barely overlapping
assert extent_iou((0, 10), (0, 10)) == 1.0
assert extent_iou((0, 10), (8, 18)) < 0.2
assert endpoint_match((0, 10), (0, 10)) == 1.0
```

The 2-D merged-shape features (error handling elided):

```python
import numpy as np
from scipy.ndimage import binary_closing
from skimage.morphology import disk
from skimage.measure import label, regionprops

def merge_shape(mask, close_radius=3):
    closed = binary_closing(mask, structure=disk(close_radius))
    cc = label(closed, connectivity=2); s = np.bincount(cc.ravel()); s[0] = 0
    r = regionprops((cc == s.argmax()).astype(np.uint8))[0]; p = max(r.perimeter, 1.0)
    return min(r.solidity, 1.0), min(4 * np.pi * r.area / (p * p), 1.0)

# true cut: two halves of one disk, 2px seam -> high solidity + compactness
g = np.zeros((40, 40), bool); yy, xx = np.ogrid[:40, :40]
disk_mask = (yy - 20) ** 2 + (xx - 20) ** 2 <= 12 ** 2
true_cut = disk_mask.copy(); true_cut[19:21, :] = False     # cut into two halves
# false merge: two separate disks side by side -> concave waist, low solidity
false_merge = ((yy - 20) ** 2 + (xx - 12) ** 2 <= 7 ** 2) | ((yy - 20) ** 2 + (xx - 30) ** 2 <= 7 ** 2)
print("true  cut :", merge_shape(true_cut))      # ~ (solidity 0.96, compactness 0.92)
print("false pair:", merge_shape(false_merge))   # ~ (solidity 0.73, compactness 0.47) - concave join
```
<img width="902" height="499" alt="shape_features" src="https://github.com/user-attachments/assets/e893d93e-108a-4967-bf41-e73df3f675c8" />


## Validation (sweep, not fit)

Weights are fixed by reasoning (flat-equal); the ground-truth fixture only **validates** them. Sweeping `min_confidence` over 3 synthetic layouts (recall = fraction of cut pieces stitched; precision = cut / (cut + intact-false-merge)):

| min_confidence | recall (5-feature) | precision | intact false-merges |
|----------------|--------------------|-----------|---------------------|
| 0.3 – 0.7      | 0.64               | 1.00      | 0                   |
| 0.8            | 0.58               | 1.00      | 0                   |
| 0.9            | 0.06               | 1.00      | 0                   |

(The recall ceiling is < 1 because not every cut piece has a stitchable partner.) **Default `min_confidence=0.7`** gives full attainable recall with zero false merges and headroom before the high-threshold drop-off. Users should still tune it for their data — the score is heuristic, not a calibrated probability.

<img width="757" height="468" alt="validation_sweep" src="https://github.com/user-attachments/assets/846a310d-952c-4ace-8cf7-214a1ca26342" />


## Obs / uns contract (consumed additively by PR-C)

- `.obs`: `stitch_group_id` (int), `is_stitched` (bool), `n_pieces` (int32), `stitch_confidence` (float64; `NaN` = not an outlier, `1.0` = evaluated-solo, composite = stitched).
- `.uns["tiling_stitch"]`: params, `score_features`, and the run counts.

PR-C's `make_stitched_labels` reads only this contract (it does not import `_tiling_stitch`).

## Notes for review

- **Codecov**: expect the patch % to dip on `_tiling_stitch.py` (defensive branches in the geometry helpers); the algorithm paths are covered by `tests/experimental/test_tiling_stitch.py`.
- **`hatch-test.py3.13-pre`**: the pre-release-deps job is a known upstream flake (pre-existing on #1170/#1188), not caused by this PR.
- **Visual test**: `TestStitchVisual` renders a seam recolour (before by `label_id`, after by `stitch_group_id`); its baseline PNG is bootstrapped from the first CI run's artifact (not generated locally).
- Also extracts three shared helpers (`resolve_params`, `equivalent_diameter` + `largest_contour`, `iter_chunked_regionprops`) into `experimental/utils/`, reused by `_tiling_qc`/`_tiling` to remove duplication. QC numerics are unchanged — the committed QC/tiling visual baselines pass.

## Out of scope

- `make_stitched_labels` + materialisation — **PR-C** (next, stacks on this).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9966fd50923`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.