# Issue

**Title:** fix(RunSpaNorm): reject invalid counts before normalization

## Description

## Problem and change

RunSpaNorm silently replaced negative and non-finite selected counts with zero. Reject invalid values before constructing backend input, including non-integer values required to be rejected by SpaNorm. Valid counts keep their values and identifiers; no rounding is introduced.

Audit evidence: [previous preprocessing at the audited commit](https://github.com/mengxu98/scop/blob/790c367fc4008acf017b92af98a2b7c0af40fc28/R/RunSpaNorm.R#L204). For example, -1/Inf became zero, while fractional values reached the backend. The integer requirement matches both locally inspected SpaNorm 1.4.0 `checkSPE` and [upstream checkers at a fixed commit](https://github.com/bhuvad/SpaNorm/blob/c12e5e57a9ee24036a32a178f1dd4466d4679ab4/R/checkers.R#L1-L14).

## Validation

- New regression was red before the fix: negative, NA, NaN, +/-Inf and fractional values were all accepted by preprocessing.
- New regression: 8 assertions pass, including valid sparse counts and reversed barcode order.
- Existing `test-run-spanorm.R`: 26 assertions pass.
- Current cloud rerun: R 4.5.0, Seurat 5.6.0, SeuratObject 5.4.0. The eight count-validation assertions and 26 wrapper assertions passed again. This supersedes the earlier Windows validation environment.

Compatibility: previously silently repaired invalid inputs now fail explicitly. Fractional values now fail before backend construction under the same strict integer contract as SpaNorm. Valid integer input and output assay behavior are unchanged.

## Current cloud validation

In addition to the wrapper regressions, a live SpaNorm backend run matched the corresponding upstream pipeline exactly. The fitting algorithm is unchanged.

## Shared Seurat compatibility follow-up

The cross-platform checks also exposed shared compatibility failures outside this spatial change. This branch now includes the common PCA/SCTransform fix:

- PCA auto fallback follows the installed Seurat implementation, including Seurat 5.6's EigenGramPCA path. Explicit backends and rank semantics are preserved; sparse-input tests assert strict upstream result/error parity.
- SCTransform handles `defer.residual.matrix` with version-aware signatures and preserves legacy `StdAssay` behavior for `do.correct.umi = FALSE` through upstream delegation.
- Neighbor tests materialize results before assertions to avoid testthat double evaluation while retaining the strict two-call check. No C++ code changes.

Cloud validation of the shared patch: PCA passed 69 assertions on Seurat 5.6 and 68 on 5.2.1; SCTransform passed 126 and 111 assertions respectively with real glmGamPoi, with no failures, errors, or skips. Seven related suites passed 333 assertions with one pre-existing optional glmpca skip. Installed lazy loading and S3 registration were checked with both Seurat versions.

## Final GitHub Actions verification

Verified on 2026-10-05 at head `397c4f0cdd6a21588a7228e32ef776205830847c`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37331023559) passed on Ubuntu, Windows and macOS, including the key Suggests job; [pkgdown](https://github.com/mengxu98/scop/actions/runs/37331023558) also passed. This PR remains open as a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `790c367fc400`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.