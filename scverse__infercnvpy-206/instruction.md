# Issue

**Title:** perf: numba kernel for tl.ithcna and tl.ithgex

## Description

Summary: `tl.ithcna` and `tl.ithgex` no longer build the cells x cells correlation matrix of each group, so they work on groups of tens of thousands of cells and run 7 to 10 times faster. The results match the previous implementation to about 1e-7.

Changes:
- Both scores are the interquartile range of the Pearson correlations between all cells of a group. Before, each group was densified and passed to `np.corrcoef` (float64), which needs `8 * n^2` bytes: 3.2 GB at 20,000 cells and 51 GB at 80,000.
- New `tl/_ith.py`:
  - The rows are standardized once: centred, scaled to unit norm, as float32, straight from CSR without a dense float64 copy.
  - For each block of 2048 rows, one BLAS product gives the correlations with all later rows (the upper block triangle only).
  - A parallel numba kernel (`njit_parallel`, nogil, with the serial twin for other threads) adds each block to thread-local histograms with about a million bins over [-1, 1]. Every pair counts twice, as in the full matrix, and the diagonal is added at the end.
  - The 25th and 75th percentiles come from the cumulative counts, with numpy's linear interpolation between ranks.
  - Groups of at most 2048 cells keep the exact float64 `np.corrcoef` path, so small groups give the same values as before.
- Behaviour change: a cell with a constant profile has no defined correlation. Before, one such cell (for example a cell without any CNV signal, an all-zero row in `X_cnv`) made the score of its whole group NaN, because `np.percentile` propagates NaN. These cells are now left out. Both docstrings have a `versionchanged` note.
- Both functions get `n_jobs`, which sets the number of numba threads, like `tl.infercnv`.

Benchmark (16 cores on the HMGU cluster, X_cnv-like data with 2000 windows and 30 % non-zero entries, one group):

| cells | new | before | difference |
|---|---|---|---|
| 5,000 | 0.12 s | 0.84 s | 9e-8 |
| 10,000 | 0.36 s | 2.83 s | 1e-7 |
| 20,000 | 1.16 s | 12.3 s | 1e-8 |
| 40,000 | 4.0 s | (13 GB matrix) | |
| 80,000 | 17.7 s | (51 GB matrix) | |

On the 10x Atera breast FFPE dataset (154k cells), `tl.ithcna` over the CNV leiden clusters took 96 s with the previous implementation.

Testing: New `tests/test_ith.py` compares the kernel with numpy for dense and CSR input, on the histogram path (several blocks) and the exact path, checks that constant cells are left out, and that fewer than two cells give NaN. The existing score tests pass unchanged. The full suite passes on the cluster (235 passed, 12 skipped), and so do prek and mypy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52d527c683e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.