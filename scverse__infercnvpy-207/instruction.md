# Issue

**Title:** feat(tl): n_pairs for ithcna/ithgex, an unbiased estimate from sampled cell pairs

## Description

Summary: `tl.ithcna` and `tl.ithgex` get an opt-in `n_pairs` argument that estimates the score of large groups from randomly drawn cell pairs. The default is unchanged: all pairs, exact.

Changes:
- Both scores are the interquartile range of the correlations between all cells of a group. With `n_pairs`, the row and the column of each sampled entry are drawn independently and uniformly, so the sample has the same distribution as the full correlation matrix, including the diagonal and both triangles. The sample quantiles are therefore unbiased estimates of the exact score, and their error shrinks like `1 / sqrt(n_pairs)`.
- This samples cell pairs rather than cells. Subsampling cells (as #192 did with `max_cells`) keeps all pairs among a random subset, and those pairs are correlated with each other, so the estimate is noisier for the same cost.
- The cost depends only on `n_pairs`: a parallel numba kernel computes the sampled correlations from the standardized rows. Groups with fewer matrix entries than `n_pairs` are computed exactly, and the log names the groups that were estimated.
- `random_state` (default 0) seeds the draws, so results are reproducible.

Benchmark (16 cores, X_cnv-like data, 2000 windows, one group):

| cells | exact | `n_pairs=1_000_000` | difference |
|---|---|---|---|
| 20,000 | 1.25 s | 0.34 s | 2.5e-5 |
| 80,000 | 16.4 s | 0.55 s | 2.4e-5 |

Testing: A new test checks that the estimate over several seeds matches the exact score and that small groups stay exact. The score tests pass on the cluster, and so do prek and mypy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3dd658514d60`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.