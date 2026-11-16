# Issue

**Title:** [3/3] Add make_stitched_labels (materialise stitched labels)

## Description

Completes the tile-cut stitching arc (`[1/3]` #1188, `[2/3]` #1193) with the materialisation step.

## Usage

```python
sq.experimental.tl.calculate_tiling_qc(sdata, labels_key="labels")
sq.experimental.tl.assign_stitch_groups(sdata, labels_key="labels")
sq.experimental.im.make_stitched_labels(sdata, labels_key="labels")
# sdata.labels["labels_stitched"]      -> pieces of a cut cell share one ID (original untouched)
# sdata.tables["labels_stitched_table"] -> one row per stitched cell
```

Knobs: `merge_strategy` (how additive user features aggregate across pieces; default `"sum"`), `join_labels` (close the seam so a group is one connected component; stays lazy on dask), `write_table`, `inplace`.

## Also in this PR

- **De-bloat** of the merged arc: inlined the single-use `utils/_geometry.py` helpers into their one caller (module deleted) and routed `_resolve_qc_params` through the shared `resolve_params`. No behaviour change.

Closes the #1170 arc.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f9d5002885f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.