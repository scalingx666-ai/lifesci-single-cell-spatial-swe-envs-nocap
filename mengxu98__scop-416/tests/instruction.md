# Issue

**Title:** feat: deprecate the `srt` alias of the data-object argument

## Description

## Summary

`SpatialSpotPlot()`, `RunSpotQC()`, `RunSpatialNetwork()`, `RunSpatialVariableFeatures()`, `SpatialVariableFeaturePlot()`, and `RunDEtest()` keep accepting `srt=`, but it now warns and is removed in scop 1.0.0 — matching the convention that the data object is `object=`.

- `resolve_deprecated_srt(object, srt, object_missing)` normalizes the alias, warns once per call with `.Deprecated()`, and rejects ambiguous `object=` plus `srt=` calls.
- `spatial_resolve_object()` reuses it.
- Rd and NEWS document the alias as deprecated; the alias test now asserts the warning.

## Validation

- `testthat::test_local(filter = "spatial-object-alias|rundetest|spatial-core|spatial-run-receipt|spatial-neighborhood-profile|standard-spatial-stages")` — all pass, and no internal call site triggers the deprecation warning.
- `roxygen2::roxygenise()` regenerates only the six affected Rd files.

## Follow-up

The remaining ~164 exported functions still take `srt` as their first formal. Extending `object` to them (with `srt` deprecated) is the package-wide migration; tracked separately.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f53dd45da6d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.