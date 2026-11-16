# Issue

**Title:** [1/3] Bundle TilingQCParams; add resolve_labels_array helper

## Description

PR 1/3 of the #1170 split. 

```python
# before
calculate_tiling_qc(sdata, "labels", distance_tol=1.0, min_area=30, max_contour_points=400)

# after
calculate_tiling_qc(sdata, "labels", tiling_qc_params={"distance_tol": 1.0, "min_area": 30, "max_contour_points": 400})
# or TilingQCParams(distance_tol=1.0, ...)
```

`adata.uns["tiling_qc"]` no longer carries flat `distance_tol`/`min_area`/`max_contour_points`; they live under `["tiling_qc_params"]`.

Also adds a private `resolve_labels_array` helper in `experimental/utils/_labels.py` (consumed here, reused by PR-B/PR-C). A strict variant of the existing `get_element_data` — fail-loud rather than fall-back, so downstream label pipelines can't silently pick the wrong scale.

PR-B will add `stitch_tile_cuts` + `StitchParams` and the QC-side warning hook. PR-C will add `make_stitched_labels`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `154abbfc9acd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.