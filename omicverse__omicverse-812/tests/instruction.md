# Issue

**Title:** feat(pp): GPU non-parametric UMAP backend (ov.utils.gpuex.umap) — replaces parametric mixed-mode UMAP

## Description

## Problem

In `cpu-gpu-mixed` mode `ov.pp.umap` used **parametric** UMAP (`pumap`, an MLP encoder). Parametric and non-parametric UMAP are different algorithms, so the mixed-mode embedding looked visibly different from CPU mode — users reported the inconsistency.

## What this does

Adds `omicverse/utils/gpuex/umap/` — a faithful GPU reimplementation of umap-learn 0.5.7's **non-parametric** UMAP (`simplicial_set_embedding` + `optimize_layout_euclidean`), and routes `cpu-gpu-mixed` UMAP to it instead of `pumap`. Same fuzzy graph, spectral init, `a/b` curve and edge-SGD update rule as CPU — only the optimisation runs on the GPU.

| file | role |
|---|---|
| `_ab.py` | `find_ab_params` (umap-learn parity) |
| `_init.py` | graph prune · `make_epochs_per_sample` · spectral init (`torch.lobpcg` on GPU, scipy `eigsh` CPU fallback) · `[0,10]` rescale |
| `_sgd.py` | torch GPU edge-SGD: analytic attractive/repulsive grads, `clip(±4)`, linear `alpha` decay, negative sampling, atomic `index_add_` |
| `_sgd_mlx.py` | Apple-Silicon (MLX/metal) edge-SGD — the same Apple path ov uses for PCA/Harmony (not torch-MPS, which lacks float64/sparse here) |
| `_embedding.py` | `simplicial_set_embedding_torch`: drop-in for umap-learn's signature; `backend='auto'` → CUDA(torch) / MLX(metal) / CPU; the connectivities COO is uploaded **once** and shared by lobpcg + SGD (no repeated host↔device transfer) |

Wiring: `ov.pp.umap` gains `method='umap-gpu'`; `cpu-gpu-mixed` mode routes to it. `n_epochs` falls back to scanpy's **500/200** (the parallel GPU SGD needs enough epochs to converge — the CPU branch's 10/20 collapses it).

## Validation (H100; pbmc3k + 100k/193k lung-atlas subsets)

- **Consistency**: trustworthiness matches CPU umap-learn — 0.8628 vs 0.8628 (pbmc3k), 0.986 vs 0.987 (100k); Procrustes within CPU's own seed-to-seed variance. (Bit-equality is impossible — different RNG + parallel updates; structural equivalence is the target and result.)
- **Speed (edge-SGD vs umap-learn)**: 28× @10k → 78× @100k → **123× @193k**.
- **GPU spectral (lobpcg vs scipy eigsh)**: **26×** (1.1 s vs 28.5 s @100k), same eigen-subspace (canonical corr > 0.99).
- **Memory**: peak **0.52 GB @100k** (sparse SpMV, never a dense n×n), CPU fallback on OOM/non-convergence.
- **Out-of-core**: works on `anndataoom` backed AnnData — UMAP is graph-based and never reads the on-disk X matrix (verified on a 193k backed object).

## Tests / CI

- `tests/pp/test_gpuex_umap.py` — torch CPU path (runs on the existing Ubuntu CI) + MLX path (skipped where metal is absent).
- `.github/workflows/gpuex-umap-mac.yml` — new **macos-14 (Apple Silicon)** job that installs MLX and exercises the metal backend. (The MLX path is written against MLX's documented API but was developed on Linux/CUDA; this job is its first real run — please watch its result.)

## Notes / follow-ups

- The standalone `ov.pp.umap` function default stays `method='umap'` (CPU); only mixed mode auto-uses gpuex.
- The CPU `method='umap'` branch still uses omicverse's 10/20-epoch default (untouched here) — separately worth aligning to 500/200.
- `pumap` backend is retained (still selectable via `method='pumap'`).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5f2b1f2870f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.