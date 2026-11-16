# Issue

**Title:** Split wnn into helpers and fix the kNN defects it worked around

## Description

Two commits, best reviewed one at a time.

## 1. Split `wnn` into helpers

`wnn` did all its work in one function. The parameter checks, the kNN search within each modality, the modality weights and the multimodal kNN now each have a helper (`_check_params`, `_modality_knns`, `_modality_weights`, `_multimodal_knn`), and the stored `random_state` comes from `_random_state_param`.

Results, errors and the order of the checks are unchanged. I compared old and new `wnn` and got identical graphs, weights and error messages, including for a NumPy float64 `sd_scale`, a pandas Series `cross_constant`, misspelled algorithms and calls with two invalid arguments. There are two intended differences:
- The warning that `random_state` is ignored for a method other than `'umap'` now points at the caller. Before, it pointed at the random-state decorator.
- `cross_constant` entries are converted to float during validation, so a bad entry fails before the kNN searches.

## 2. Fix the kNN search defects that `wnn` worked around

`pp.neighbors` and `pp.bbknn` had three kNN defects that `wnn` worked around on its own:

- **Incomplete approximate searches.** Approximate searches can leave neighbor slots unfilled. IVF repeats an ID at an infinite distance around small clusters, CAGRA returns out-of-range IDs and `all_neighbors` pads with `sqrt(FLT_MAX)`.
  - Before, `pp.neighbors` stored these as infinite distances and NaN connectivities, or failed inside cuML with `method='umap'`. For example, `algorithm='ivfflat'` with default settings on 2,000 cells with small clusters gave 125 infinite distances at 15 neighbors.
  - Now `_check_knn_complete` raises a `ValueError` after every search in `pp.neighbors`, `pp.bbknn` and `wnn`. The message suggests a fix for the algorithm used, e.g. raising `n_probes` for IVF. It replaces `wnn`'s own check.
- **nn_descent failed above 96 neighbors**, cuVS's default `intermediate_graph_degree`. That degree now defaults to `max(96, 1.5 * k)` and is raised to at least `k`, so results are unchanged up to 64 neighbors. `wnn`'s own default is removed.
- **CAGRA failed above 64 neighbors**, its default `itopk_size`. The search width is now `max(64, k)`, so results are unchanged up to 64 neighbors. `itopk_size` is a new `algorithm_kwds` option. `wnn`'s limit of `knn_range <= 64` for CAGRA is removed.

## Notes for review

- **nn_descent recall above 64 neighbors.** cuVS's nn_descent loses recall once the graph degree passes 64, whatever `intermediate_graph_degree` is. I measured about 0.97 at 64 neighbors, 0.81–0.89 at 100 and 0.63–0.73 at 150. So the fix stops the crash, not the quality loss, and the new test only requires a recall of 0.7 for nn_descent (0.9 for CAGRA).
- **CAGRA's upper limit.** CAGRA kept a recall of at least 0.995 up to 600 neighbors. From about 800 neighbors, cuVS returns invalid IDs at any search width, and the new check now turns them into an error.

## Tests

- New tests in `tests/test_neighbors.py`:
  - nn_descent and CAGRA at 100 neighbors, checking recall against brute force;
  - an incomplete IVF search, which must raise and leave `adata` unchanged;
  - `pp.neighbors` and `bbknn` given padded IDs, infinite distances or NaN distances, which must raise.
- `tests/test_wnn.py` now also runs CAGRA at the default `knn_range` and no longer expects the old CAGRA limit.
- `tests/test_neighbors.py`, `tests/test_mg_neighbors.py` and `tests/test_wnn.py` pass locally (104 tests).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e93ec98095e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.