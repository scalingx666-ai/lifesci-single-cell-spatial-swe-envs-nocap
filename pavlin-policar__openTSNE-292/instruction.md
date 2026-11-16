# Issue

**Title:** Fix HNSW and Annoy distance scales and self-removal

## Description

Prepares HNSW to become openTSNE's default nearest-neighbor backend and fixes the matching correctness issues in Annoy. Every kNN backend now reports distances on the same scale as exact search. The default method is **not** changed here.

## HNSW
- **Euclidean distances were squared.** hnswlib's `l2` space returns squared distances, and the affinity code squares them again (`_tsne.pyx:64`), so perplexity calibration saw d⁴. On 70k MNIST (PCA-50) the L1 difference between HNSW-based and exact P was 0.141 before and 0.0004 after.
- **dtypes:** HNSW now returns int64 indices and float64 distances, matching the other backends (hnswlib gives uint64/float32).
- **Self-removal by index:** `build` used to drop the first column. With duplicate points, or under `ip`/`dot`, that kept the point itself and dropped a real neighbor.
- **`ef = max(2k, 100)`**, overridable with `knn_kwargs={"ef": ...}`. Small-k queries (`transform`) had recall of 0.77 at k=1 and 0.96 at k=5; they now reach ≥0.999 for every k.
- **`n_jobs`** is resolved the scikit-learn way: hnswlib treated `-2` as all cores. Seeded builds with more than one thread now warn, because hnswlib's parallel build is nondeterministic (2192 of 20k rows differed between runs).
- Docstrings describe HNSW's metric semantics, its `knn_kwargs` and its reproducibility.

## Annoy
- **`cosine`** returned angular distance `sqrt(2 − 2cos)`. It now returns `1 − cos`, the same as exact search.
- **`dot`** returned the raw inner product, a similarity, so the most similar neighbors got the smallest affinities. It now returns `1 − ⟨x,y⟩`, the same as HNSW and pynndescent; this is correct for normalized data.
- **Self-removal by index**, shared with HNSW through `_exclude_self`.

## Behavior changes
- Results change for HNSW with `euclidean`/`l2`.
- Results change for `cosine` and `dot` under `annoy`, and also under `auto`/`approx`, which route dense data with these metrics to Annoy.
- Results change for data with duplicate points under both Annoy and HNSW.

## Recall@90 vs exact search (current defaults, 8 threads)
| Dataset | HNSW | Annoy |
|---|---|---|
| MNIST PCA-50, 70k | 0.9994 (3.3 s) | 0.9896 (6.5 s) |
| MNIST raw 784, 20k | 0.9990 (7.5 s) | 0.9609 (7.8 s) |
| Macosko PCA-50, 45k | 0.9903 (1.5 s) | 0.9418 (3.2 s) |
| Gaussian blobs d=50, 100k | 0.9893 (6.2 s) | 0.9390 (9.4 s) |

## Tests
New tests in `tests/test_nearest_neighbors.py`:
- Euclidean distances match `cdist`, and dtypes are consistent, for every backend.
- HNSW matches exact search for euclidean, l2 and cosine.
- Annoy cosine and dot distances.
- Duplicate points and inner-product self-removal for both backends.
- HNSW `ef`, `n_jobs` and the reproducibility warning.

Each fix's tests fail without the fix. Locally: 193 passed, 21 skipped in the main env, where numba can't import with numpy 2.5. The nearest-neighbor and affinity tests also pass in a venv with numpy 2.3 and pynndescent 0.6.0 (100 passed). Azure CI installs both hnswlib and pynndescent.

## NNDescent
- Distances are now float64 (pynndescent returns float32). The conversion is lossless, so values are unchanged. The shared dtype test caught this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e95b40f6c6e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.