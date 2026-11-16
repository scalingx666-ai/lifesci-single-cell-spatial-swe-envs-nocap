# Issue

**Title:** feat: complete parameter coverage for masked Seurat functions

## Description

## Summary

An audit of scop's masked Seurat functions (`NormalizeData`, `ScaleData`, `FindVariableFeatures`, `RunPCA`, `RunUMAP`, `RunCCA`, `FindNeighbors`, `FindMarkers/`FindAllMarkers`, `FoldChange`) found two crashes and three hard-error gaps. This PR fixes all of them **with native implementations, not fallbacks**:

- **FoldChange crash fix**: register a thin `FoldChange.Seurat` method — the masked generic previously dispatched Seurat objects into `FoldChange.default` and crashed.
- **RunCCA crash fix**: `cca_crossprod_matrix` / `matrix_product` were declared in C++ and called from `RunCCA.default` but never exported; both now get `// [[Rcpp::export]]` wrappers.
- **NormalizeData**: implements `CLR` (margins 1 and 2) and `RC` alongside LogNormalize. The CLR denominator follows native semantics exactly: \`exp(sum(log1p(x[x>0])) / length(x))\` — denominator over the *full* slice length.
- **ScaleData**: supports `vars.to.regress` + `latent.data`, `split.by`, `use.umi` (residuals shifted per-gene then log1p, matching `RegressOutMatrix`), `do.scale = FALSE`, and custom `scale.max`. Regression runs per split group like the native sources document.
- **FindVariableFeatures**: supports `disp` and `mean.var.plot` using Seurat's own `FastExpMean`/`FastLogVMR` internals for numeric parity.

## Validation (native vs scop)

| Branch | result |
|---|---|
| NormalizeData Log/CLR×2 margins/RC | max diff 8.9e-16 / **0.00e+00** / 4.5e-13 |
| ScaleData regress / split.by / use.umi / use.umi+regress / do.scale=F / scale.max=3 | ≤ 8.9e-16 each |
| FVF disp & mean.var.plot | Jaccard = 1.000 |
| FoldChange masked call | identical values |

Note on `ScaleData(vars.to.regress=..., split.by=...)`: the combined path was arbitrated against Seurat's own exported internals — scop matches the documented per-group `RegressOutMatrix` + `FastRowScale` composition exactly; this Seurat version's composite wrapper deviates from its own building blocks for that combination (verified by calling them separately).

New tests: `tests/testthat/test-seurat-coverage.R` (13 assertions) plus existing regression suites stay green (120 assertions total across sctransform/seurat-coverage/choir).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de047e5c373d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.