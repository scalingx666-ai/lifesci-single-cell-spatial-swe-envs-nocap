# Issue

**Title:** fix: report SpotSweeper artifact status truthfully

## Description

## Summary

- distinguish per-sample SpotSweeper artifact states as completed, skipped, failed, or not_requested
- use NA and NotEvaluated for artifact or local-outlier output that was not actually produced
- mark the overall run partial whenever any requested spot/stage remains unevaluated, while preserving known Fail precedence
- validate fresh binary artifact and local-outlier producer outputs instead of accepting stale or non-binary metadata
- require findArtifacts() to retain every input spot identity and order; shortened, renamed, or reordered output fails that sample truthfully
- reject missing sample labels and producer-owned name collisions before optional-backend checks
- preserve sample.by encounter order and original sample spot counts in stored diagnostics
- reject return_filtered = TRUE whenever requested QC is incomplete, before mutating the returned object
- keep all recoverable partial paths returnable under options(warn = 2) through a non-success, non-warning console channel

## Validation

- PASS: latest-head macOS, Ubuntu, and Windows R-CMD-check
- PASS: latest-head pkgdown and changes jobs
- PASS: latest Codex review found no major issues; all eight review threads are resolved
- PASS: full test-run-spotsweeper.R targeted file, including missing/partial/invalid/stale output, non-binary flags, dropped/renamed/reordered spots, missing sample labels, reserved names, and return-filtered atomicity
- PASS: parameterized warning-escalation coverage under options(warn = 2)
- PASS: focused real SpotSweeper 1.5.0 run on 120 bundled Visium spots; the upstream-incompatible artifact stage returned a truthful partial result with 120 NotEvaluated calls
- PASS: pkgload::load_all('.', quiet = TRUE, compile = FALSE)
- PASS: prescribed local rcmdcheck on the final implementation: 0 errors, 2 inherited warnings, 5 notes
- PASS: checking for unstated dependencies in examples and tests
- PASS: R/Rd parse and git diff --check

The two local check warnings are inherited from upstream main: lifecycle / glmGamPoi / sctransform namespace declarations and pre-existing Rd usage mismatches. This PR does not modify those dependency or Rd topics.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06a934438d9b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.