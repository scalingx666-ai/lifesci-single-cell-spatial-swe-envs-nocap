# Issue

**Title:** fix: forward the data object under `object` only

## Description

.

## Cause

`RunDoubletCalling()` resolved the deprecated `srt` alias and then forwarded its matched formals, so the selected doublet backend received **both** `object` and `srt` and stopped at its own alias check: "Provide only one of `object` or `srt`". `RunCellQC()` dispatches with `object=`, so it failed for every `db_method`, while a direct `RunDoubletCalling(srt=)` call only survived because the internal variable holding the resolved object happened to be named `srt` — the `match.call()` merge re-evaluates the caller's expressions in the callee frame.

The same leak hit the Python bridges: their Python functions accept neither `object` nor extra keywords, so `object=<Seurat>` came back as `unused argument (object = ...)`.

## Changes

- `RunDoubletCalling()` resolves into `object`, forwards the resolved object under `object` only, and drops the merged `srt` entry. The `db_rate` default and the error message use the canonical name.
- `RunSCVELO()`, `RunCellRank()`, `RunPalantir()`, `RunPAGA()`, `RunWOT()`, and `RunCellTypist()` keep `object` out of the argument list they send to Python, next to the existing `srt` entry. Both entries are needed until the `srt` formal is removed in 1.0.
- `RunCellphoneDB()`, `RunIntegration()`, and the app scaffolding needed no change (explicit whitelist or no data-object alias).

## Tests

- `RunDoubletCalling()` forwarding is covered for both dispatch branches (`Scrublet` and the two-part `scds_cxds`) and for the deprecated `srt=` form.
- The bridge tests replace `function(...)` mocks — which swallowed the extra argument and hid the regression — with a mock that rejects `object`/`srt`, plus `object=` coverage for `RunPAGA()` and `RunWOT()`.

## Verification

- test-run-cell-qc, test-python-backend-tools, test-cellrank-palantir-closure, test-paga-cpp, test-cpp-backend-safety all pass.
- The new guards fail on the unpatched code (3 failures + 5 errors).
- `RunCellQC(srt=)`, `RunCellQC(object=)`, and `RunDoubletCalling(db_method = "scds_cxds")` return results with the expected `db.*` columns.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `64bcbfe508a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.