# Issue

**Title:** feat: add concise spatial run receipts

## Description

## Summary

- add one internal spatial run-receipt renderer; no exported API, registry, result schema, history, environment switch, or new global option
- pilot concise Done / Scope / Saved / Plot-or-Inspect receipts in RunSpotQC, RunSpatialNetwork, RunBayesSpace, and RunSpatialVariableFeatures
- use an explicit <returned_object> placeholder instead of guessing the caller's assignment name
- report analysis separately from retention: full tool result, assay VariableFeatures only, both, or neither
- keep receipt facts aligned with the returned object, including Assay5 cell subsets and metadata-backed outlier metrics
- preserve three-state SpotQC semantics for finite, failed, and unevaluated outlier rules; known Fail takes precedence, otherwise unresolved requested QC remains NA/NotEvaluated
- validate outlier aggregation/cutoffs and give a clear error when filtered output would contain no spots
- emit plot hints only when they are executable: select hires when lowres is invalid, use raw/result-only Network plotting, BayesSpace metadata Inspect, or SVF summary fallbacks when display scales are unavailable
- fall back to the dependency-free SVF summary plot when optional patchwork is unavailable, without installing it
- skip all receipt-only image/coordinate probes when effective verbosity is disabled

## Console shape

```text
✔ Spot QC completed: 120 evaluated, 120 Pass, 0 Fail
ℹ   Scope assay "Spatial", layer "counts"
ℹ   Saved metadata column `SpotQC`
ℹ   Plot returned object `SpatialSpotPlot(<returned_object>, group.by = "SpotQC")`
```

The placeholder is intentional: an R function cannot reliably discover an outer assignment target. The receipt therefore provides an honest template and explicitly names the returned object instead of hard-coding a variable that may not exist.

## Validation

- PASS: latest-head macOS, Ubuntu, and Windows R-CMD-check
- PASS: latest-head pkgdown and changes jobs
- PASS: latest Codex review found no major issues; all review threads are resolved
- PASS: installed-package smoke on 120 bundled Visium spots: SpotQC 120/120 Pass; KNN graph 120 nodes/280 edges; native R Moran SVF 100 tested/10 top; all three suggested plots built; store_results = FALSE retained only VariableFeatures and emitted Inspect without a false tool/Plot claim (1.97 s)
- PASS: test-spatial-run-receipt.R (132 expectations), including Assay5 subsets, noncontiguous/reordered cells, finite/NA/Inf rule aggregation, exact counts, filtering, quiet paths, storage combinations, and executable hints
- PASS: Network display-scale receipt tests, BayesSpace receipt/backend tests, full native spatial-variable-feature tests, spatial coordinate contract v2, spatial core, workflow stage, and SPOTlight dispatch tests
- PASS: package fallback test proving SVF summary remains executable when patchwork is unavailable
- PASS: pkgload::load_all('.', quiet = TRUE, compile = FALSE)
- PASS: prescribed final local rcmdcheck: 0 errors, 2 inherited warnings, 4 notes; unstated dependencies in examples and tests both OK
- PASS: R/Rd parse and git diff --check

The two local check warnings are inherited from upstream main: lifecycle / glmGamPoi / sctransform namespace declarations and pre-existing Rd usage mismatches. This PR does not modify those dependency or Rd topics.

## Validation boundary

BayesSpace adapter behavior is covered with a mocked backend; this PR does not claim a new live upstream BayesSpace integration run. The receipt is deliberately a thin rendering of facts already validated by each producer, not a second result framework.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06a934438d9b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.