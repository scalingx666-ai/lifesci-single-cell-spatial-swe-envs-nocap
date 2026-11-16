# Issue

**Title:** feat: integrate official CellOracle perturbation analysis

## Description

## Summary

SCOP can now run the official CellOracle 0.20.0 workflow on Seurat objects and retain its perturbation results for R plotting. `RunCellOracle()` delegates PCA, imputation, GRN inference/filtering, simulation-model fitting, perturbation and projection to CellOracle; it does not substitute SCOP's GRN inference or reimplement the algorithms.

- Support prepared Linux/macOS Python environments and an already-running Linux Docker container, allowing Windows R to round-trip inputs and results without initializing host Python.
- Accept official TF-info tables/parquet files or target-to-TF dictionaries; preserve non-log fractional counts accepted by upstream. Validate cell/gene order, numerical outputs and saved-model compatibility before write-back.
- Save/reload official Oracle and Links models. Reject existing result names/output directories. Require explicit environment preparation.
- Add `CellOraclePlot()` for cell displacements, official grid flow/masks, randomized controls, descriptive expression effects and directed cluster networks; preserve reciprocal regulatory edges.
- Add an isolated Python 3.10 environment profile, generated help, reference-index entries and regression tests. Docker children fix the standard Python hash seed to the supplied seed because upstream set-derived predictor ordering affects bagging coefficients.

## Validation

- 38 new R assertions passed; existing environment-requirements tests passed with one pip-availability skip.
- `pkgload::load_all('.', quiet=TRUE, compile=FALSE)` passed.
- `_R_CHECK_FORCE_SUGGESTS_=false` with `rcmdcheck::rcmdcheck(args=c('--no-manual','--as-cran','--no-examples','--no-tests'), error_on='never')`: 0 errors, 0 warnings, 3 notes (CRAN incoming checks, existing maintainer-field mismatch and existing unqualified `tail`). R-code dependency and unstated-example-dependency checks both passed. The package check intentionally excluded tests/examples; targeted R tests and separate real-backend scripts were run.
- Installed unmodified CellOracle 0.20.0 in an isolated Linux container; `pip check` passed. Core versions: NumPy 1.26.4, pandas 1.5.3, SciPy 1.11.4, scikit-learn 1.2.2, AnnData 0.10.8, Scanpy 1.9.8.
- Compared the adapter with direct official calls on constructed data and an official Paul2015 subset (140 cells, 260 genes; Ery_0/Ery_1; original force-directed coordinates; official mouse ATAC base GRN). With matched parameters and random/hash seeds, maximum absolute differences were **0** for imputed/simulated expression, delta_X, cell/randomized displacements, grid/randomized flow, density and both clusters' network coefficients. The actual Windows R -> Docker -> Seurat path also matched direct official output exactly; saved-model reuse reproduced the expression, cell and grid results exactly.
- `git diff --check` passed. Automatic `styler::style_file()` was unavailable because styler is not installed.

## Scope and limitations

The real-data subset is an engineering parity test, not a biological claim; upstream warnings about the small gene/TF set remain visible. Data, installed environments, checkpoints and validation outputs stay outside the package. Fresh conda provisioning and a complete native Linux R session were not tested end-to-end; the prepared Docker path was. CI results are separate from these local checks.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8288c84cc972`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.