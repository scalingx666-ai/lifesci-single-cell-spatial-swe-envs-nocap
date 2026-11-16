# Issue

**Title:** fix: keep Presto runtime optional

## Description

## Summary

- remove the GitHub-only Presto package from Suggests while retaining `immunogenomics/presto` in Remotes
- centralize the repository, package name, non-installing availability check, and `wilcoxauc` resolution in runtime-optional helpers
- let automatic marker paths use an existing Presto installation without installing it, and fall back to Seurat when the backend is unavailable
- resolve `wilcoxauc` with `get_namespace_fun()` once per marker entry point and inject the resolved function into computation workers
- route the supported `RunCellChat(do.fast = TRUE)` path through the same centralized availability helper
- harden function resolution so a NULL namespace lookup is treated as a missing backend symbol
- separate real-backend tests from always-on fallback tests, and run a required source-mode Presto smoke before the `--as-cran` library restriction hides Remotes-only packages
- merge the complete spatial workflow/receipt series from current `main` and revalidate the combined package

## Why the CI test is split

`R CMD check --as-cran` restricts package tests to Depends, Imports, Suggests, and their transitive dependencies. Because Presto is intentionally Remotes-only, it is correctly unavailable inside that restricted test process even when setup-r-dependencies installed it in `R_LIBS_USER`.

The workflow therefore verifies the real GitHub installation before `R CMD check`. That required source-mode step asserts that `wilcoxauc` resolves, executes its current API, and drives the supported SCOP `FindMarkers()` / `FindAllMarkers()` paths. Inside `R CMD check`, real-backend parity blocks skip only when Presto is hidden, while mocked availability, non-installing fallback, RunCellChat, and DESCRIPTION contracts always run.

## Validation on combined head `e806e6be`

- PASS: clean merge of current `main` (`d925a0b6`, including PR #391); final topic diff remains the intended 11 Presto files
- PASS: `test-presto-backend.R`, `test-rundetest-findmarkers.R`, and `test-seurat-fast-paths.R` with `compile = TRUE`
- PASS: seven exact source-mode parity descriptions each matched and executed exactly one test (`COMBINED_SOURCE_PRESTO_PASS=7`)
- PASS: `env_r_packages()` contains exactly one `immunogenomics/presto`
- PASS: Presto absent from Depends, Imports, Suggests, LinkingTo, and NAMESPACE; retained only in Remotes
- PASS: no direct `presto::` / `presto:::`, `requireNamespace("presto")`, `library(presto)`, or `require(presto)` in executable package code
- PASS: marker fast paths resolve an existing install without installing; `RunCellChat(do.fast = TRUE)` may install/check only when its upstream API supports the fast parameter
- PASS: `pkgload::load_all('.', quiet = TRUE, compile = FALSE)`
- PASS: prescribed local `rcmdcheck(... --no-manual --as-cran --no-examples --no-tests)`: **0 errors, 2 inherited warnings, 4 notes**
- PASS: `checking for unstated dependencies in examples ... OK`
- PASS: `checking for unstated dependencies in tests ... OK`
- PASS: dependency scan contains no Presto warning; only the inherited `lifecycle` / `glmGamPoi` / `sctransform` warning remains
- PASS: `git diff --check`; generated Rcpp EOL rewrites were removed and the worktree is clean

Presto 1.1.0 still exports `wilcoxauc` with compatible `X`, `y`, and `verbose` parameters and the expected result columns. The initial remote failure was the expected `--as-cran` dependency isolation, not an upstream API regression.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d925a0b6a35e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.