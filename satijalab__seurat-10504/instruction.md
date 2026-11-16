# Issue

**Title:** Fix `FindSpatiallyVariableFeatures` cell lookup for `FOV` spatial images

## Description

This PR proposes changes based on  but with a narrower scope.

# Summary

`FindSpatiallyVariableFeatures()` assumed `rownames(spatial.location)` were cell names. For FOV-backed data such as CosMx/Xenium/Vizgen-style objects, GetTissueCoordinates() can return coordinates like:

|     | x   | y | cell |
|-----|-----|---|------|
| 1   | ... |   |      |
| 2   | ... |   |      |
| ... |     |   |      |

(That is, with integer row names and the real cell IDs in the cell column.) The `Assay`/`StdAssay` method then used row names like 1, 2, 3 to pull expression data, found no matching cells, produced a matrix with zero columns, and passed that to RowVar(), which could segfault.

Both this PR and 10457 address the core bug by using the cell column as coordinate row names before moving down the method dispatch. There are also two small fixes in both PRs that address other issues:  resolving the `selection.method` argument with `match.arg()` and fixing the wrong `nfeatures = nfeatures` default in `FindVariableFeatures.Assay/StdAssay` to `nfeatures = 2000`.

This branch proposes an additional safeguard on the cell column prior to using it as rownames: we check for duplicates, which occur when the default boundary for the selected image as segmentation-based. In that case, multiple coordinate rows can refer to the same cell (where each row represents coordinates for one vertex of the segmentation polygon). If this is true, users are directed to choose a centroid-based boundary or provide `spatial.location`.

The test added to `test_spatial.R` covers the assay-specific FOV case and also explicitly checks the segmentation boundary path.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4b718c54b08`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.