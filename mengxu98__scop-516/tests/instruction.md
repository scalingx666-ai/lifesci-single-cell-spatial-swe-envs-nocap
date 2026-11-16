# Issue

**Title:** fix: restore exponential count recovery for sparse inputs

## Description

`RecoverCounts(trans = "exp")` fails on log-normalized input because Matrix exponentiation returns a dense `dgeMatrix`, while the recovery code subsequently reads the sparse `@p` slot.

Restore `dgCMatrix` storage after the transformation and before scale-factor inference and count recovery. Apply the transformation to the complete matrix first, preserving `exp(0) = 1` for implicit zeros. No function signatures, transformation choices or recovery heuristics change.

Add regression coverage for sparse and genuinely dense Assay5 inputs, legacy Assay objects, explicit and inferred scale factors, implicit zeros, single-cell dimensions, non-default assays, count metadata, invalid transformations and unsuccessful recovery. Record the fix under the development version in NEWS.

Validation:
- Reproduced the missing `@p` error on unchanged main using the real data-type detector; the same reproducer now recovers the expected counts.
- All 54 tests and 348 assertions across the recovery, Seurat fast-path, Seurat consistency and dispatch-contract suites pass, with no warnings or skips. The new recovery tests account for 53 assertions.
- 27 whole-object comparisons against the original function preserve `expm1`, `none` and raw-count behavior across sparse, dense and legacy inputs.
- `R CMD build --no-build-vignettes --no-resave-data` passes.
- Tested on macOS with R 4.5.3, Matrix 1.7-6, SeuratObject 5.4.0 and Seurat 5.5.0. Source tests reused the compiled library from identical native sources; a full `R CMD check` was not run.

Prepared from clean main in a separate worktree. This PR contains only the recovery fix, its tests and NEWS; it excludes the primary checkout's existing uncommitted changes and the separate simplification work in #515.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `033bf280ea26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.