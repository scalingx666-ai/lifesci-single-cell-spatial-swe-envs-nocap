# Issue

**Title:** feat: support grouped fits in DynamicPlot

## Description

## Summary

- add an optional `fit.by` metadata column to `DynamicPlot()` without changing the existing positional API
- fit each selected group independently while preserving the existing overall-fit behavior when `fit.by = NULL`
- draw group-specific fitted lines and confidence intervals over each group’s observed pseudotime range without extrapolation
- retain raw points and rugs for groups, features, and unassigned cells that do not meet the default GAM support threshold
- check finite observations, unique pseudotime values, and usable library sizes independently for every feature before fitting
- use collision-safe internal columns and tuple identities for grouped paths without overwriting user metadata
- keep linetype assignments stable across separate lineage or feature panels
- apply built-in and function-valued transforms over a shared per-lineage comparison scope
- cap grouped transformed infinities consistently per feature and lineage
- preserve user metadata named `FitGroup` and other helper-like names through collision-proof internal columns
- keep grouped colors and legends consistent across factors and multiple panels
- preserve feature/lineage identity with linetypes in grouped line and interval-only panels
- reject more than six combined grouped series instead of recycling linetypes
- deduplicate raw points and rugs across compared lineages
- allow `RunDynamicFeatures()` count-layer fits with a custom `libsize` vector

## Validation

- `devtools::test(filter = "dynamic", stop_on_failure = FALSE)`: 74 passed, 0 failed, 0 warnings, 0 skipped
- grouped-fit coverage: 56 passed, including all twenty-nine Codex review regressions
- real `pancreas_sub` smoke: grouped lines and interval-only plots both preserve two group encodings and two feature linetypes with complete legends
- real GAM support smoke: a count feature with insufficient positive custom library sizes is skipped only in the affected group while the supported group remains fitted
- all-unassigned synthetic smoke: all 24 raw points remain visible without fitted trajectories
- `tools::checkRd("man/DynamicPlot.Rd")`: passed
- `styler`: all four newly touched source/test files unchanged
- `git diff --check`: passed
- the previous full local suite reached an unrelated network-dependent `cccdb` failure because Ensembl was unavailable; GitHub macOS, Windows, Ubuntu, and pkgdown checks passed on preceding grouped-fit commits

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `36e4cf186574`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.