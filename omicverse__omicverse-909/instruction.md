# Issue

**Title:** feat(monocle2): support residual model batch correction

## Description

## What changed

- add `residualModelFormulaStr` to the public `ov.single.Monocle.reduce_dimension()` API
- build a Patsy design matrix from `adata.obs` and remove modeled non-intercept effects before dimensionality reduction
- record residual-model provenance in `adata.uns['monocle']['residual_model']`
- validate missing values, intercept-free formulas, rank-deficient designs, and zero-variance ordering genes
- add focused unit and integration coverage and declare the Patsy runtime dependency

## Why

Monocle 2 supports residual-model formulas for removing technical covariates during trajectory construction, but the OmicVerse Monocle implementation did not expose equivalent behavior. This adds opt-in batch/covariate correction while preserving the existing uncorrected default.

## User impact

Users can now run, for example, `mono.reduce_dimension(residualModelFormulaStr='~ sampleID')`. Existing calls without a formula are unchanged.

## Validation

- Monocle 2 test suite: **100 passed, 3 skipped**
- exercised on a 1,848-cell Colon subset with 17 samples; sample-associated pseudotime effect decreased substantially after correction

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d050a5e75021`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.