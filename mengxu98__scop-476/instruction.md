# Issue

**Title:** refactor: narrow Seurat and ggplot2 imports

## Description

## Summary

Replace the broad Seurat and ggplot2 namespace imports with explicit imports for the functions and values SCOP uses. Import SeuratObject generics from their defining package and retain the existing thisplot/thisutils imports.

The import set also preserves dynamic theme lookup and the GSEA line-plot path: string theme names such as `theme_minimal` still apply their requested arguments, and the GSEA background bands retain their `alpha()` color conversion. Regression tests cover all ten standard theme constructors and building a GSEA line plot.

Public exports, S3 registrations, function interfaces, defaults, and algorithms are unchanged. No new dependency or fallback layer is introduced.

## Validation

- Static function/value lookup audit found no missing symbols previously supplied by Seurat/ggplot2; public exports and method registrations are unchanged.
- Clean-session smoke tests passed for NormalizeData, FindVariableFeatures, ScaleData, RunPCA, CellDimPlot, S3/S4 dispatch, and package unload/reload without attaching Seurat or ggplot2.
- Theme tests and an actual GSEA line-plot/build regression passed. These tests reproduce and prevent the missing-theme and missing-alpha regressions found during review.
- The earlier full suite reported 13 failures, 311 warnings, 40 skips, and 8,513 passes. The theme failure is fixed; ten other failures reproduce identically on unmodified upstream and this branch. The Presto failure passes in isolated runs on both; Ensembl connectivity is a separate limitation. This is not a claim of a clean local full suite.
- A combined local rehearsal of the independently proposed refactors passed 128 targeted cases (565 passing expectations, 0 failures/errors, 1 CRAN-guarded skip), followed by the final GSEA line-plot regression.
- Required `pkgload::load_all(".", quiet = TRUE, compile = FALSE)` passed.
- The exact `_R_CHECK_FORCE_SUGGESTS_=false` check with `--no-manual --as-cran --no-examples --no-tests` stopped during CRAN incoming feasibility because `Meta/archive.rds` timed out; its zero-count summary is not a successful check.
- Supplementary check without `--as-cran` completed: 0 errors, 2 warnings, 1 note. Existing warnings are the local missing `thisplot::NetworkPlot` / `thisutils::fit_trends` exports and six undocumented `RunSingleR` arguments; the note concerns `PKG_CFLAGS`. Compilation, install, load/unload, startup suppression, S3 consistency, compiled code, and unstated example dependencies passed. Examples/tests are excluded by this check command and are covered separately above.
- `git diff --check` passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d7d9fb7976d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.