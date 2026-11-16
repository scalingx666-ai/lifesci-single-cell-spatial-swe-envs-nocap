# Issue

**Title:** fix: preserve numeric FeatureHeatmap annotations and handle missing values

## Description

When a numeric metadata column is used both as a cell annotation and as `group.by` or `split.by`, `FeatureHeatmap()` currently converts it to a factor before building annotations. Preserve the original annotation metadata so it retains a continuous color mapping while grouping and splitting remain categorical.

Numeric annotations with no finite values among the plotted cells now render in grey with a `Missing` legend instead of failing with `'from' must be a finite number`. Non-finite values in partially observed numeric annotations use the existing transparent missing-value color.

Validation:
- Added regression tests covering shared grouping/splitting columns, cell-name alignment, all-missing and non-finite annotations, selected-cell missingness, and unchanged factor annotations.
- New annotation tests and the existing projection/heatmap border tests pass locally against the changed source.
- Generated before/after plots using identical data and plotting parameters for shared split/annotation columns and all-missing annotations.
- `git diff --check` passes.

The reported blank annotation from the user's original object remains under investigation; a controlled cell-name mismatch reproduced that appearance, but the original object has not been supplied. This change addresses the independently reproduced cases above.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `75450a5d7f3d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.