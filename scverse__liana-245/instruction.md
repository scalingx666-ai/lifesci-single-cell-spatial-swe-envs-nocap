# Issue

**Title:** Fix LRIC performance and memory issues

## Description

Performance and memory improvements for `CrossPCF` and `LRIC` 

**CrossPCF**

- Pre-compute a `cKDTree` once per cell type before the pair loop; previously a new tree was built for every directed pair.
- Replace `n_bins` sequential `query_ball_point` calls per pair with a single `sparse_distance_matrix` call returning all within-range distances at once. Bin assignment is then done via `np.searchsorted` rather than `(n_edges, n_bins)` boolean masks.
- `_corrected_areas`: cells farther from the bounding-box edge than the outermost radius have all annuli fully inside the box and receive the exact analytical area without angle sampling. Only boundary cells call `_circle_bbox_fractions`.
 
**LRIC**

- Adopts the same `sparse_distance_matrix` and `_corrected_areas` interior/boundary optimisations. Removes the `_spatial_pairs` helper (was `query_ball_point` loop + `np.linalg.norm`).
- Rewrites `_lric_bins` to avoid the `(n_edges, n_pairs)` dense cross-weight matrix that caused a `MemoryError` on large datasets. The new approach builds a sparse `(n_recv, n_send)` scale matrix per annulus bin and multiplies it against the weight matrices in `pair_chunk`-wide column slices. Peak memory is bounded to a few hundred MB regardless of dataset size.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `348f943e4740`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.