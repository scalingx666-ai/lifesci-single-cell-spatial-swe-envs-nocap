# Issue

**Title:** fix: handle missing optional GSVA in native scoring probes

## Description

## Summary
Release CI only has GSVA in Suggests. `gsva_standardize()` called `packageVersion("GSVA")` without a read-only probe, and `gsva_uses_legacy_sparse_walk()` used `requireNamespace("GSVA")`, so sparse `RunGSVA(..., method = "zscore", backend = "cpp")` could fail when GSVA is absent.

## Changes
- Probe GSVA with `check_r("GSVA", install = FALSE, verbose = FALSE)`.
- If missing: standardize `TRUE`, legacy sparse walk `FALSE` (GSVA >= 2.6 defaults); if installed, keep version gating.
- Remove `requireNamespace("GSVA")` from these probes.
- Add sparse C++ zscore/PLAGE numerical tests that work without GSVA; keep the existing ssgsea species-alias coverage.
- NEWS under the development version.

## Test plan
- [x] Targeted styler/parse checks and 50 assertions including real probes with GSVA absent (Codex).
- [ ] CI R-CMD-check / Suggests jobs on this PR.

Branch: `fix/gsva-optional-probe` @ `c31785d`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24f4698989b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.