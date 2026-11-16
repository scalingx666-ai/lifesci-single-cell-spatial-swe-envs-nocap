# Issue

**Title:** perf(gpuex/umap): on-device negatives + sum-before-scatter in MLX backend (1.6x → ~2.5x on M2)

## Description

## What

Two profiling-guided changes to the MLX (metal) edge-SGD in
`omicverse/utils/gpuex/umap/_sgd_mlx.py` that lift the Apple-Silicon UMAP
speedup from **1.6× to ~2.5× vs CPU**, with **identical trustworthiness**.

## Why

Profiled `optimize_layout_mlx` on a real 50k-cell fuzzy graph (200 epochs,
~352k active edges/epoch) on an Apple M2. Two avoidable costs dominated:

1. **Negative sampling ran on the host every epoch** — `np.repeat` of the
   catch-up counts + `np.random` over millions of vertices, then a
   host→metal transfer. Measured at **~31% of runtime**, capping the metal
   speedup at ~1.6×.

2. **Negative gradients were scattered as `A*n_neg` updates.** All `n_neg`
   negatives of an anchor land on the *same* vertex, so the scatter-add
   atomics (the dominant GPU cost) were `n_neg`× larger than necessary.

## How

1. Draw a fixed `round(negative_sample_rate)` negatives per active edge
   **directly on metal** with `mx.random` — the standard GPU/cuML
   simplification; umap-learn's catch-up schedule averages to the same
   rate. Removes the host RNG and the per-epoch index transfer.
2. **Sum the `n_neg` negative gradients per anchor before scattering** →
   `A` scatter updates instead of `A*n_neg` (5× fewer atomics at n_neg=5).
3. Minor: reuse one fractional `pow` in the attractive term; gather the
   negative rows once.

Active-edge selection stays on the host (`np.nonzero` over the schedule is
only a few % and avoids re-touching the ~70% of edges inactive in a typical
epoch). An all-edges static-shape loop under `mx.compile` was tried and was
**measurably slower** on real graphs (~3.4× the work) and can't trace the
dynamic scatter with `shapeless=True` anyway — see the module docstring.

## Results (Apple M2)

| | before | after |
|---|---|---|
| `optimize_layout` (isolated, real graph, thermal-controlled) | 6.5s | **3.5s** |
| end-to-end bench (incl. CPU spectral init) | — | MLX ~4.6s vs CPU ~11.4s |
| **speedup vs CPU** | 1.6× | **~2.5×** |
| trustworthiness | 0.9776 | **0.9776 (unchanged)** |

Memory-neutral (`mx.eval` per epoch, ~140 MB at 50k cells). An
`eval`-every-K pipeline reaches ~3.05s but needs ~1 GB at 50k cells
(scales with dataset size) — deliberately not the default.

## Test

`tests/pp/test_gpuex_umap.py` passes (4 passed), including
`test_mlx_embedding_preserves_structure` (asserts
`abs(tw_mlx - tw_cpu) < 0.05`). `bench_gpuex_umap.py 50000` reproduces the
numbers above.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb3038d209a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.