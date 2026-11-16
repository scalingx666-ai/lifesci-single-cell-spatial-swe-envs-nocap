# Issue

**Title:** Per-batch clip threshold leaks across batches in `_highly_variable_pearson_residuals`

## Description

In `_highly_variable_pearson_residuals`, the default clip threshold is computed inside the per-batch loop guarded by `if clip is None`. Because the assignment writes back to the `clip` parameter itself, the guard is only true on the first iteration; every subsequent batch reuses the first batch's threshold instead of computing its own.

Lause, Berens & Kobak (2021) define the clip as `sqrt(N)` on the cell count entering the residual computation, so with `batch_key` the correct value is `sqrt(n_cells_in_batch)`. On a 5000/200 split, the 200-cell batch silently inherits `sqrt(5000) ≈ 70.7` instead of `sqrt(200) ≈ 14.1`. Residuals in the small batch that should be clipped are not, its per-gene variance is inflated, and HVG ranking shifts. The output also depends on `np.unique`'s alphabetical ordering of batch labels, so renaming `"A"` to `"B"` (and vice versa) on otherwise identical data changes the HVG list — not the kind of reproducibility surprise one wants buried in a preprocessing default.

The fix introduces a loop-local `clip_batch` so the per-batch default is recomputed each iteration; the user-facing `clip` parameter is left alone. Two tests cover it. `test_pearson_residuals_batch_clip_scoped_per_batch` monkeypatches the `csc_hvg_res` / `dense_hvg_res` bindings and asserts that two distinct clip values reach the kernel across batches — on the buggy code both calls receive the same value. `test_pearson_residuals_batch_order_invariant` swaps `A`↔`B` on identical data and checks that `residual_variances` matches bit-for-bit. Both fail on the unpatched code; the rest of the pearson + HVG suite (58 tests) still passes. Verified on an H100.

scanpy ports this routine almost verbatim and carries the same bug — I have a parallel PR open at scverse/scanpy#4138 with the same one-line scoping fix and equivalent CPU-side tests. Happy to land them together, or to hold this one until the scanpy side merges, whichever you prefer.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32c424ab3f71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.