# Issue

**Title:** fix: preserve ATAC label-transfer identities and result provenance

## Description

## Summary
Fix the existing ATAC-to-RNA `RunLabelTransfer` path. This is independent of #497 and the proposed new downstream APIs; it targets current `main` directly.

- Use a reversible temporary query-ID map for native Seurat anchors and weights, then require complete unique predictions and restore original cell IDs/order. On Seurat 5.5.1, IDs containing `_query` previously caused either a silent missing label (39/40 cells) or duplicate native row-name errors.
- Record actual anchor features and current prediction columns. Treat prefixes literally, remove only columns owned by the prior matching tool result, and reject overwriting unrelated metadata.
- Preserve caller RNG, including absent-seed and error paths, without adding dependencies. Keep public arguments/positional calls and the object-returning shared reference-mapping helper compatible.
- Replace the leakage-prone example with separate synthetic reference/query cells and explicit synthetic ACTIVITY input. This is a technical example and does not establish biological accuracy.

## Validation
R 4.4.3 / Seurat 5.5.1 / SeuratObject 5.4.0 / Signac 1.16.0. On the current main base `8339f62`, normal package installation rebuilt all 46 C++ translation units. Installed related regression tests: **17 cases / 138 assertions**, zero failures, errors, warnings or skips. The generated public example executed successfully; installed function bodies/formals match source. Source tests: 7 cases / 44 assertions, zero failures, errors, warnings or skips. Real Seurat FindTransferAnchors/TransferData comparisons cover disjoint and cross-object identical IDs, `_query` collisions, factor labels, reordered valid queries and Idents, source preservation, actual features, prefixes, and reruns. Independent code review passed on the four-file candidate.

## Scope
Four files only: implementation, generated help, regression tests and NEWS. No API export/dependency changes. No automatic invocation of the unmerged RunGeneActivity wrapper.

## Package-check boundary
On the previous main base `f089f714` only, ordinary offline `R CMD check --no-manual --no-examples --no-tests` completed: **0 errors, 2 warnings, 6 notes**. Tests and the public example were executed separately as above; this is not a full-package test-suite or `--as-cran` result. The first check session was interrupted without a terminal result; its log was retained and a separate recovery check completed normally. The cancelled incoming/network `--as-cran` step was not retried.

That previous-base check reported warnings: existing GCC 16 `velocity_utils.h` string-overflow diagnostic and six undocumented `RunSingleR` arguments. Notes: unavailable pre-existing optional packages, package size, existing spatial `tail` namespace diagnostic, optional-package help references, UTF-8 data, and Makevars flags. Relevant source files were hash-compared to unchanged main; no separate full baseline check is claimed. No new diagnostics concern this change. Hosted CI will be reported independently.

The new main base includes the upstream SingleR documentation fix. The old local check is not claimed as a check of this rebased tree. Current-base installed regressions/example are rerun; hosted full CI for the new head is tracked separately.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8339f62cdf83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.