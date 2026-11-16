# Issue

**Title:** perf(preprocess): fuse normalize_total + Pearson-HVG Pass-1 (in-memory path)

## Description

## Summary
- `ov.pp._normalization.normalize_total` now computes per-gene totals + per-gene `E[count²]` alongside its existing per-cell-sum pass, and stashes the four-tuple in `adata.uns['_pearson_precompute']`.
- `ov.pp.experimental._highly_variable_pearson_residuals` auto-consumes that dict (single-batch case) and skips its own Pass 1.

## Why
`ov.pp.preprocess(mode='shiftlog|pearson')` makes the in-memory path scan the raw counts matrix twice:

1. `normalize_total` reads X for per-cell sums.
2. `highly_variable_pearson_residuals` reads X again for per-cell + per-gene + sum_total.

Both functions are fully local (no scanpy in the hot path — `omicverse.pp._normalization` and `omicverse.pp.experimental._highly_variable_genes` are independent implementations), so the redundancy is removable without touching upstream.

## Numerical equivalence
A new regression test (`tests/pp/test_pearson_precompute_fusion.py::test_hvg_pearson_fast_path_matches_legacy`) runs HVG selection both with the precompute auto-consumed and with it disabled on identical input, and asserts `np.testing.assert_allclose(residual_variances, atol=1e-9, rtol=1e-10)` plus identical `highly_variable` masks.

## Skip-stash conditions
The precompute is deliberately NOT written when it would carry stats inconsistent with what downstream sees:
- `exclude_highly_expressed=True` — per-cell sums get overwritten on a filtered subset (a third pass).
- per-batch HVG (`batch_key` set) — the global stash doesn't split per-batch.

In both cases the legacy two-pass behavior runs.

A staleness guard on the HVG side rejects precompute dicts whose `n_obs`/`n_vars` don't match the current adata (covers the case where the caller var-subsets between normalize and HVG).

## Expected savings
TS-1M (1,053,033 cells × 60,606 genes) is OOM-killed today on the in-memory path (separately addressed by omicverse#804 `use_implicit_centering`). Once that unblocks, preprocess on the OOM backend goes from 1874 s → ~1300 s with this fusion (~30%). For the in-memory path, same fusion applies — savings scale with `nnz(X)`.

## Companion (anndataoom)
The OOM backend gets the same fusion in . The two PRs are independently mergeable; each backend benefits on its own.

## Test plan
- [x] 4 unit tests (`test_normalize_stashes_precompute`, `test_hvg_pearson_fast_path_matches_legacy`, `test_subset_invalidates_precompute`, `test_exclude_highly_expressed_skips_precompute`). All passing locally.
- [ ] CI.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7f7086c490bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.