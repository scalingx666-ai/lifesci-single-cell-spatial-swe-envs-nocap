# Issue

**Title:** fix: normalize species names before database lookup

## Description

## Problem and change

`RunGSVA(..., db = "MSigDB_H", species = "homo_sapiens")` fails with `no input has determined the number of cases`: `PrepareDB()` returns the canonical `Homo_sapiens` key, while the caller indexes it using the original spelling.

Normalize species names before database lookup in `RunGSVA()`, `CellScoring()`, `RunDynamicEnrichment()`, `RunCellRankEnrichment()`, `AnnotateFeatures()` and `RunMetabolism()`, including the metabolism database helper. These entry points now reuse the existing normalization rules for case, whitespace, dots and hyphens. This also prevents silent annotation omissions and unavailable-database results in related callers. `RunEnrichment()`, `RunGSEA()` and `GeneConvert()` already normalize species names.

## Validation

- Reproduced the original GSVA error and related failures before the fix with fixed annotation fixtures.
- New regression file: 32 assertions pass, covering grouped and single-cell GSVA, combined databases, scoring, feature annotations, CellRank, dynamic enrichment and metabolism outputs.
- Seven existing related test files pass; CellRank fixtures emit matrix coercion warnings.
- Revalidated on the latest `origin/main` using `Rscript --vanilla` and `pkgload::load_all(compile = FALSE)`. Reused the existing local native library after checking that native sources and Rcpp bindings are unchanged.
- `git diff --check` passes. User data/cache validation and a full `R CMD check` were not run.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3d1006781f55`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.