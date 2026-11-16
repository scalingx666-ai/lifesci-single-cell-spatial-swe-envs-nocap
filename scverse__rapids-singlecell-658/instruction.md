# Issue

**Title:** Fix float64 precision loss in sparse Pearson residual kernels

## Description

## Summary

The CSR and CSC Pearson residual kernels in `src/rapids_singlecell/_cuda/pr/kernels_pr.cuh` divide by `sqrtf`, the **single-precision** square-root intrinsic. Both kernels are templated on the element type `T`, so a `T=double` instantiation silently narrows the variance term `mu + mu * mu * inv_theta` to `float32`, evaluates the square root at single precision, and promotes the result back to `double`.

As a result, the float64 path of `pp.normalize_pearson_residuals` (and `pp.highly_variable_genes` with `flavor='pearson_residuals'`) was capped at ~7 significant digits regardless of the requested dtype. The dense kernel `dense_norm_res_kernel` already uses the overloaded `sqrt` and was unaffected.

The fix replaces `sqrtf` with the overloaded `sqrt` on both sparse paths. `sqrt` dispatches to the single-precision root for `T=float` and the double-precision root for `T=double`, so **the float32 path is byte-identical to before** and only the float64 path changes.

## Verification

A standalone harness compiled the real `sparse_norm_res_csr_kernel` verbatim and ran it on a 4000_4000 synthetic CSR count matrix against a host float64 reference (NVIDIA H100 80GB HBM3, CUDA 12.6, `sm_90`):

| dtype | before fix | after fix |
|---|---|---|
| `double` | max rel. error `8.83e-08` (~7.1 digits) | max rel. error `3.97e-16` (~15.4 digits) |
| `float`  | _ | bit-identical (max abs diff `0.0`) |

The float64 path is now ~8 orders of magnitude more accurate; the float32 path is provably unchanged.

## Changes

- `_cuda/pr/kernels_pr.cuh` _ `sqrtf` _ `sqrt` in `sparse_norm_res_csc_kernel` and `sparse_norm_res_csr_kernel`.
- `tests/test_normalization.py` _ adds `test_normalize_pearson_residuals_float64_precision`, which pins the float64 CSR/CSC output to an analytic float64 reference at `rtol`/`atol` `1e-9` (tight enough to fail on a single-precision result, pass on a genuine float64 one) across `theta` in `{100, inf}`.
- `docs/release-notes/0.15.1.md` _ bug-fix entry.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61eda66c2b27`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.