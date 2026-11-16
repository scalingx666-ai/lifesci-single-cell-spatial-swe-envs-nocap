# Issue

**Title:** Fix dynamic call history and metadata argument collisions

## Description

Seurat fallback calls now retain distinct canonical command-history entries instead of overwriting anonymous command keys. Dynamic PCA and RareQ neighbor calls keep input objects out of captured call text. Integration records canonical anchor and integration names, with a bounded correction for Seurat's internal warning-handler logging frame.

Metacell grouping and LIANA sample-key construction now treat metadata column names as data, including names shared with `interaction()` or `paste()` options. Gene-immune and SCENIC correlation tests call `cor.test()` directly to avoid expanding full vectors into discarded descriptions while retaining the same statistics.

This covers the 18 affected call sites across 10 R files, adds nine regression tests, and records the changes in the development/unreleased NEWS section.

Validation on R 4.5.3 / macOS arm64 with Seurat 5.5.0 and SeuratObject 5.4.0:

- Fresh compilation, source installation, and package loading succeeded using current main's dependency and build configuration.
- The new dispatch tests passed 90 assertions. Together with nine related existing test files, focused regressions passed 666 assertions with no failures or errors. One Python conversion test was skipped because anndata/scipy were unavailable; two existing fixture warnings were reviewed.
- The new 90 assertions also passed using the previous `invoke_fun()` implementation, so the related thisutils optimization is not a merge prerequisite.
- Tests cover canonical Seurat history, LogNormalize and its Log alias, actual TFIDF/rlsi integration, PCA values, both RareQ verbosity paths, metadata option-name collisions, and all three correlation methods. LIANA tests confirm successful native C++ results rather than silent R fallback.
- RareQ and SuperCell external algorithm boundaries are isolated with test doubles; complete Python model fitting was not exercised. Full R CMD check remains for CI.

Related:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b2489cf500d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.