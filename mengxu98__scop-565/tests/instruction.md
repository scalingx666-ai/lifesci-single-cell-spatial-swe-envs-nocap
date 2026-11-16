# Issue

**Title:** fix: prevent RunPAGA sparse-array neighbor failures

## Description

## Summary

Fix the large-data `RunPAGA()` failure caused by Scanpy 1.11.3 receiving a SciPy `csr_array` from PyNNDescent 0.7.0 while its neighbor-search path calls the matrix-only `getnnz()` API.

- Pin `pynndescent==0.6.0` in the shared Scanpy environment profile, including dependent scVelo and CellRank profiles.
- Detect a loaded PyNNDescent version that differs from its installed distribution and request an R-session restart after dependency updates.
- Keep dependency resolution and real 8,200-cell Seurat → AnnData → PAGA → Seurat regression coverage in `tests/testthat`.
- Discover an existing Python interpreter without an environment-variable skip guard, pass that interpreter explicitly into the isolated R child, and avoid installing dependencies or recompiling package sources from the integration test.
- Cover the runtime guard with unloaded, matching, and stale module states before running the real analysis.

No public R API, numerical algorithm, backend selection, package version, or CI workflow changes.

## Current validation (Windows, R 4.5.2)

Validated the test update at `eeee2160a` using existing environments; no dependency installation or environment modification was performed.

- Dependency resolution: 156 assertions passed; one existing metadata test skipped because the `python3` executable did not provide pip.
- Real 8,200-cell Seurat roundtrip: 12 assertions passed with Python 3.11.15, Scanpy 1.11.5, PyNNDescent 0.6.0, SciPy 1.17.1, and AnnData 0.12.10. Cell order, grouping, graph dimensions, symmetry, finite values, bounds, and PAGA write-back were checked. Runtime guard scenarios also completed.
- Exact pinned Scanpy 1.11.3 / PyNNDescent 0.6.0 / SciPy 1.15.3 stack: the actual bundled Python `PAGA()` completed on 8,200 constructed cells in a standalone Python 3.10.19 process, including neighbor search, PAGA graph, plotting, and draw_graph. The resulting graph passed shape, finite-value, and nonempty checks.
- Reproduced the reported `csr_array.getnnz` exception directly in Scanpy 1.11.3; the equivalent `csr_matrix` input succeeded.
- `pkgload::load_all(".", quiet=TRUE, compile=FALSE)` completed. The local testthat build emits an R-version warning (built under 4.5.3).
- R CMD check with `--no-manual --no-examples --no-tests` and `_R_CHECK_FORCE_SUGGESTS_=false`: **0 errors, 0 warnings, 1 NOTE**. Both R-code dependency checks and unstated example dependency checks were OK. The NOTE concerns globals in untouched enrichment/spatial code.
- The required `--as-cran` invocation was attempted but stopped after remaining at CRAN incoming feasibility; that check is **incomplete**, not passing.
- `styler::style_file()` and `git diff --check` passed.

## Remaining limitations

The Windows R/reticulate roundtrip using the existing Scanpy 1.11.3 `scop_env` returned NULL from its child process and failed the assertions. The cause is not established; standalone Python on that same environment passed, and the complete R roundtrip on the existing Scanpy 1.11.5 environment passed. This is not presented as an exact-stack R integration pass. No new Linux execution was performed in this update; the earlier PR history records Linux reproduction and validation at the previous head.

GitHub Actions jobs remain blocked by an account billing lock and do not execute their steps. Resolve that external restriction and rerun existing workflows before merging. Full package tests and examples are not claimed as passing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13fff459ec41`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.