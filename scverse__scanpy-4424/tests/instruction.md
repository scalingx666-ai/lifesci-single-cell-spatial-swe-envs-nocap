# Issue

**Title:** perf: numba kernels for pp.harmony_integrate

## Description

This replaces the NumPy hot loops of `sc.pp.harmony_integrate` with parallel numba kernels. With the settings the current code uses, the output is the same up to rounding (float64: relative L2 per PC ≤ 2e-12). The new defaults are 6–8× faster in float64 and 7–13× in float32.

### What changes

- `_harmony/_kernels.py` (new): one fused kernel per clustering iteration (soft assignment, held-out counts, objective parts and next centroids in a single pass over each block), and the correction statistics and apply step. Kernels take their dtype from the input, so float32 and float64 both compile.
- `_harmony/core.py`: a `harmonize` driver replaces the `Harmony` class. One correction path handles any number of batch keys: per cluster, the covariate with the most levels is eliminated in closed form and only the small Schur complement is solved (float64; it has no cell dimension). `_correction_fast` is gone; `_correction_multi` keeps its signature and now runs this path, so the existing dense-design test (1e-11 in float64) exercises the production code.
- Results do not depend on the thread count: every parallel sweep uses 32 fixed chunks.
- All-zero cells are left out with a warning and returned unchanged (they have no direction on the unit sphere).
- Crossed batch keys: per-level statistics, solve in chunks of 8 clusters. Memory no longer scales with the number of joint categories.

### New parameters (defaults first)

| parameter | values | what it does |
|---|---|---|
| `seeding` | `"afkmc2"`, `"kmeans"`, `"kmeans++"`, `"paper_nearest"` | initial centroids; `"kmeans"` is the current behaviour |
| `stop_rule` | `"reference_record"`, `"reference"`, `"paper"`, `"paper_window3"` | `"reference"` is the current behaviour (round objective recorded only when clustering converged); `"reference_record"` records every round, as rapids-singlecell does |
| `penalty_combine` | `"product"`, `"sum"` | how several keys' diversity penalties combine; `"sum"` is the rule as printed in Patikas et al. 2026 |
| `seeding_lloyd_steps` | `0` | spherical Lloyd steps on the seeds |
| `seeding_cells_per_cluster` | `None` | subsample for KMeans seeding / Lloyd steps |
| `recompute_counts` | `True` | rebuild the per-batch cluster counts every iteration instead of only updating them incrementally |
| `low_memory` | `False` | drop one cells × PCs buffer; identical result |

**Default change:** `seeding="afkmc2"` and `stop_rule="reference_record"`. The coordinates change (per-PC r 0.965–0.985 against the current output), but integration quality does not (table below). `seeding="kmeans", stop_rule="reference"` reproduces the current output.

### Benchmarks

Apple M-series, 8 threads, one batch key, `dtype=float64` unless noted, numba compiled outside the timing:

| dataset | cells | current | new, current settings | new defaults | new defaults, float32 |
|---|---|---|---|---|---|
| pancreas | 16k | 2.48 s | 0.63 s | 0.47 s | 0.35 s |
| COVID lung | 116k | 18.04 s | 3.13 s | 2.30 s | 1.51 s |
| HLCA core | 585k | 75.07 s | 11.84 s | 8.79 s | 5.79 s |

Two batch keys on HLCA (`sample` + `dataset`), where the current code spends most of its time in the multi-key correction: float32 304.8 s → 6.3 s (the new code takes 9.5 s in float64). On Linux (Intel Xeon 6248R and AMD EPYC 9745, OpenBLAS and MKL, float32, one key), HLCA takes 1.7–3.9 s at 32 threads. Memory scales linearly, about 1 GB per million cells at 50 PCs in float32.

Integration quality, current → new defaults (float64; float32 agrees to 4 decimals):

| dataset | batch mixing | cell-type purity |
|---|---|---|
| pancreas | 0.5611 → 0.5671 | 0.9731 → 0.9719 |
| COVID lung | 0.7040 → 0.7043 | 0.8868 → 0.8865 |
| HLCA core | 0.6451 → 0.6448 | 0.9014 → 0.9003 |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc97bc01668f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.