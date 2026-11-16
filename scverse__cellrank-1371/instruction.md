# Issue

**Title:** ci: fix red CI on main (zarr pin, heatmap baseline, scanpy 1.13)

## Description

## Problem

CI has been red on `main` since the start of August, blocking the **All tests pass** gate on every PR. Three independent causes:

1. **`PETSc / SLEPc + R`** (conda job) — fails at conftest import:
   ```
   ModuleNotFoundError: No module named 'zarr.core.dtype'; 'zarr.core' is not a package
   ```
   The job installs cellrank (`pip install -e '.[plot]'`, pulling **anndata 0.13.2**, which requires **zarr>=3.1**), then the next line force-downgrades to `'zarr<3'`. anndata 0.13 imports `zarr.core.dtype`, a **zarr-v3-only** module, so the downgrade breaks the whole job. The pin dates to #1291 (Feb 2026), when anndata still supported zarr v2 — it's now stale.

2. **All `hatch-test` stable legs** (Linux 3.12/3.14 and macOS) — `TestHeatmap::test_heatmap_genes` fails with RMS 67.4 against a 50 tolerance, identically on all three. The baseline was rendered with matplotlib 3.11.0; **3.11.1** (in the env since the 2026-08-01 scheduled run) shifts the `constrained_layout` placement of the `genes`-mode heatmap. The plotted content is unchanged — only the layout moved.

3. **`hatch-test.py3.14-pre`** — collection of the entire suite fails:
   ```
   ModuleNotFoundError: No module named 'scanpy.plotting.palettes'
   ```
   **scanpy 1.13.0a1** moves the legacy plotting API under `scanpy.plotting.legacy`. cellrank reached into two private scanpy symbols: `palettes.vega_20_scanpy` and `_utils.add_colors_for_categorical_sample_annotation`.

## Changes

- **Drop the `zarr<3` pin** in the conda job and let anndata resolve zarr (>=3.1).
- **Refresh the `heatmap_genes` baseline**, promoted from the Linux `py3.12-stable` `rendered-figures` artifact as `docs/contributing.md` prescribes. Reviewed against the old baseline: same curves, same ordering, same colour mapping — layout offset only.
- **Stop importing scanpy's private plotting internals** rather than chasing their new location. The palette is a fixed reordering of matplotlib's `tab20`, so it now lives in `_utils/_colors.py`, pinned by a test (the committed figure baselines depend on those exact values, and it is byte-identical to scanpy's `vega_20_scanpy` in both 1.12 and 1.13). The colour assignment is what cellrank's own `_get_categorical_colors` already did for the plotting functions, so that helper moves from `pl/_utils` to `_utils/_colors` — `models/` can't import from `pl/` without a cycle — and gains the one behaviour scanpy's helper contributed: regenerating palettes that are too short or not colour-like.
- **Keep the macOS leg blocking.** The pyGPCCA `brandts` failures that originally motivated `continue-on-error` for macOS no longer reproduce — on the latest `main` run macOS is green apart from the shared baseline drift, so it stays a gating job.

## Verification

Locally on Linux, both matrix envs pass the full suite: `py3.12-stable` (matplotlib 3.11.1, scanpy 1.12.3) and `py3.14-pre` (scanpy 1.13.0a1), the latter having previously failed at collection. The refreshed baseline is byte-identical to what this machine renders.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd555e15cb88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.