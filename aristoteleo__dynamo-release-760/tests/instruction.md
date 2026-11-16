# Issue

**Title:** Make preprocessing robust to small / degenerate adata

## Description

## Summary
Fixes the small-adata preprocessing crashes reported by @AlexanderCaichen in **#616**, with regression tests. Reproduced each on current master.

## Bugs fixed (each reproduced → crash on master)
| case | master | fix |
|---|---|---|
| few cells (e.g. 10×200) | `ValueError: k must satisfy 0 < k < min(A.shape)` in truncated SVD | ✅ `X_pca` produced |
| no gene has a finite SVR score | `IndexError: index -1 is out of bounds` (`np.sort([])`) in `get_svr_filter` | ✅ empty selection + warning |
| no gene passes the PCA filter | `InvalidParameterError: n_components ... Got -1` | ✅ PCA skipped + warning |
| a layer has no valid genes (empty `valid_CM`) | divide-by-zero in SVR / missing `score` column → `KeyError` downstream | ✅ all-invalid scores → graceful skip |

## Changes
- **pca.py** `_truncatedSVD_with_center`: `n_components = min(n_components, min(X.shape) - 1)`.
- **pca.py** `pca()`: `if 0 in X_data.shape: warn; return` (no genes).
- **utils.py** `get_svr_filter()`: graceful empty return when no finite score.
- **gene_selection.py** `calc_dispersion_by_svr()`: on empty `valid_CM`, write all-invalid (`-inf`) score columns and `continue` (this refines #616's approach — using `-inf` routes an empty gene set into the graceful abort above rather than selecting arbitrary genes).

## No regression
Normal-size preprocessing is **bit-identical** to master: `X_pca` and `use_for_pca` unchanged (`max|Δ| = 0`). My changes only add branches that don't trigger for normal data. Adds `test_pca_small_adata`, `test_get_svr_filter_no_finite_scores`, `test_pca_no_genes_pass_filter`.

. Reported by @AlexanderCaichen.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01AD7gAdxa3Zt5uiQVDoANa5

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b6e21e1248fb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.