# Issue

**Title:** feat(scale): use_implicit_centering=True for million-cell in-memory pipelines

## Description

## Summary
- Adds `use_implicit_centering=True` opt-in to `ov.pp.scale`. When set on a sparse CPU adata, the scaled matrix is stored as an `anndataoom.CenteredSparseArray` in `adata.uns['_scaled_implicit']` instead of being materialised into `adata.layers['scaled']`.
- `ov.pp.pca` (both the in-`_preprocess` dispatcher and the deeper `_pca.pca`) learns to recognise the implicit wrapper and densify only the HVG slice the SVD actually consumes.

## Why
`ov.pp.scale` on a sparse adata densifies via the sparse-zero-centering step `(X − μ)/σ`. Cost: `n_obs · n_vars · 4 bytes`. The cellxgene Tabula Sapiens benchmark measured:

| dataset | n_obs | scale stage Δ RSS | result |
|---|---|---|---|
| TS-Stromal | 232 684 | +64 GB | completes (peak 99 GB) |
| TS-Epi    | 228 032 | +66 GB | completes (peak 107 GB) |
| TS-Immune | 592 317 | — | **OOM-killed at 256 GB cap** |
| TS-1M     | 1 053 033 | — | **OOM-killed at 256 GB cap** |

At 1M cells × 60 606 genes the dense scaled matrix alone is ~240 GB — the in-memory pipeline cannot run on a typical commodity node regardless of how fast PCA is.

The OOM backend (`anndataoom`) already side-steps this with a lazy `ScaledBackedArray`. This PR ports the same design to in-memory by wrapping the scale output in a sparse-backed `CenteredSparseArray` that holds `(X/σ : sparse CSR, μ/σ : ndarray)`. Per-gene access materialises only the requested rectangle and stays bit-equal to the textbook reference; `@ W` matmuls go through the identity `(X − μ)/σ · W = (X/σ) · W − (μ/σ) · W` used by `chunked_pca` path 2.

## End-to-end validation
TS-Vasc (42 650 × 36 554, the standard cellxgene Tabula Sapiens slice in our bench):

| path | scale | pca | total | peak RSS | cos(50 PCs) |
|---|---|---|---|---|---|
| dense (default) | 22.7 s | 4.9 s | 27.5 s | 26.7 GB | baseline |
| `use_implicit_centering=True` | 6.7 s | 52.7 s | 59.4 s | **16.3 GB** | **1.0000 / 50** |

TS-10k full panel: dense peak 7.0 GB → implicit 3.2 GB. Cosine 1.0000 on all 50 PCs.

Per-component cosine equals 1.0000 because the per-element materialisation at the consumer boundary preserves the textbook `clip((X − μ)/σ, -∞, max_value)` operator exactly. The implicit path is slower at small sizes because sklearn picks a different SVD solver between float32 (implicit) and float64 (dense layer view) inputs — `covariance_eigh` on float64 outpaces randomized SVD on float32 when `n_features ≪ n_samples`. The flag is opt-in: default dense path stays the small-data winner.

## Requirements
- Companion PR `omicverse/anndata-oom#6` lands `CenteredSparseArray` and exports it from `anndataoom`. This PR's flag raises `ImportError` with a clear pointer when the prereq is missing.

## Test plan
- [x] TS-10k full panel: cosine 1.0000 / 50, RSS 7.0 GB → 3.2 GB.
- [x] TS-Vasculature 42 k: cosine 1.0000 / 50, RSS 26.7 GB → 16.3 GB.
- [ ] TS-Immune (592 k) full pipeline — was OOM-killed in the dense path; running this PR with `use_implicit_centering=True` to confirm completion. Result will be appended in a follow-up comment.
- [ ] CI on existing test matrix.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7f7086c490bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.