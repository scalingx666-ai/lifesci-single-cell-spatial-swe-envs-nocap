# Issue

**Title:** Fix/perf and variability optimizations

## Description

Summary

  This PR introduces significant performance optimizations to Palantir’s core routines and provides an optional high‑velocity kNN backend. On standard datasets (~4k cells), these changes reduce total execution time by ~51% in default parity mode and ~65% in “fast” mode.

  Core Improvements

  - Algorithmic optimization: _max_min_sampling complexity reduced from $O(N \cdot K^2)$ → $O(N \cdot K)$ as waypoint count (K) scales.
  - Vectorized pseudotime: replaced per‑waypoint shortest‑path loops with a single vectorized csgraph.dijkstra call; iterative refinement now runs in pure NumPy.
  - Memory‑aware entropy: chunked sparse LU solves for differentiation entropy to avoid large dense allocations.
  - Backend flexibility: added kernel_backend="sklearn" in run_diffusion_maps for throughput‑oriented runs; default remains scanpy for parity.

  Numerical Stability & Parity

  - Default behavior: scanpy backend preserves prior behavior.
  - Fast mode: minor drift in higher components (~1e‑3) due to kNN graph differences, while DC1 correlation stays at 1.000000 (primary axis preserved).

  Benchmarks (real data, marrow_sample_scseq_counts.h5ad; 4,142 cells /
  2,000 genes)

  | Mode | Total | run_palantir | diffusion_maps | PCA |
  |------|-------|--------------|----------------|-----|
  | Scanpy (default/parity) | ‑51% (3.25s vs 6.69s) | ‑73% | ‑22% | ‑7% |
  | Sklearn (fast) | ‑65% | ‑72% | ‑98% | ‑5–8% |

  Validation (sklearn vs scanpy):

  - eigenvalues_max_abs: 3.247e‑03
  - eigenvectors_min_abs_corr: 0.986981
  - dc1_abs_corr: 1.000000

  Notes

  - Benchmark scripts and tooling are maintained on the branch but excluded from
    this PR to keep the core library lean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c3decacf17c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.