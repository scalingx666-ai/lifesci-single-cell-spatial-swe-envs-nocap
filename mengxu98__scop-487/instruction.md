# Issue

**Title:** refactor: split CCCHeatmap data and layout helpers

## Description

## Summary

- Keep the public `CCCHeatmap()` entry point and main rendering flows in `R/CCCHeatmap.R`.
- Move matrix and interaction data preparation helpers to the existing `R/ccc-data.R`.
- Move the shared matrix renderer and annotation/layout helpers to the existing `R/ccc-plot-utils.R`.
- Preserve the single-use CCCHeatmap helpers already placed in `R/CCCHeatmap.R` by merged PR #471.
- The integration source split was merged separately in PR #475; this PR contains only the remaining CCCHeatmap organization.

## Behavior and API

- Parsed the 107 function definitions in the affected CCC files before and after relocation; all formals and function bodies are identical.
- No exported API, result shape, algorithm, plotting options, execution order, `NAMESPACE`, `DESCRIPTION`, or dependency declarations changed.

## Validation

- `Rscript -e 'pkgload::load_all(".", quiet=TRUE, compile=FALSE)'`: passed.
- Existing CCC and integration test files passed: heatmap helpers, CellChat consistency, CCC platform/backend parity, spatial CellChat, SpaTalk, integration helper/dispatch, and Assay5 coverage. One Python conversion case was skipped because `anndata` and `scipy` are unavailable.
- A representative `ccc_matrix_heatmap_plot()` call returned a patchwork object.
- Requested Windows `rcmdcheck` completed with 0 errors, 2 warnings, and 4 notes. The warnings are from unchanged code/docs: `thisplot::NetworkPlot` and `thisutils::fit_trends` references, and undocumented arguments in `RunSingleR.Rd`. The examples dependency check reported OK; examples and the full test suite were disabled for that command.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `215fe4141015`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.