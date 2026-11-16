# Issue

**Title:** fix(spatial): correct coordinate graphs, HD units, and result context

## Description

PRECAST integration can build an empty graph by treating full-resolution image pixels as Visium array indices, and can fit the default assay instead of the requested matrix. Visium HD communication also inherits the ordinary Visium 65-micron calibration, while SVG surfaces can silently switch assays after analysis.

This change:

- Builds PRECAST inputs from the selected, validated counts. The default graph uses SCOP's shared exact spatial KNN implementation, adapted to PRECAST's column-neighbor convention; it avoids the [native single-axis candidate restriction](https://github.com/feiyoung/PRECAST/blob/main/src/getNB_fast.cpp) and records the graph builder, arguments and edge counts.
- Rejects incompatible array-index adjacency, invalid/empty graphs, and missing or non-finite integration outputs before storing results.
- Requires calibrated `ratio` and observation-appropriate `tol` for Visium HD, recognizes HD import/bin evidence, and preserves spot/bin semantics for VisiumV2 images inheriting FOV.
- Makes SVG surfaces inherit saved assay/layer/image/coordinates, validates backend feature IDs and p/q values, and uses the complete supplied p-value family when filling missing BH-adjusted values.

Roxygen/Rd, NEWS and workflow documentation are synchronized. DESCRIPTION and dependency declarations are unchanged; no environment or global-option switches are added. These changes apply to new runs: rerun affected PRECAST/HD analyses to replace existing results.

Validation:

- 19 targeted test files: 210 cases, 1,726 passing assertions, zero failures/errors (Seurat/FOV/key warnings remain).
- Full real Visium slice: 1,986 spots, 11,916 nonzero KNN entries; every selected neighbor independently checked against the sixth-nearest Euclidean distance, allowing boundary ties, and every strictly closer spot required to be present. The old array-index default produced zero edges on this slice.
- Raw analysis coordinates remain identical after a tenfold display-scale change. Long-row and axis-swap/translation regressions verify exact geometry and matrix orientation.
- Real PRECAST 1.8: two regions of a real slice, 120 spots/60 genes, successful fit/storage/plots; backend coordinates and counts match selected spot IDs. This is an API fixture, not independent biological replication.
- HD calibration/preflight is covered by regression tests; a full real-HD communication inference was not rerun.
- R CMD check (`--no-manual --as-cran --no-examples --no-tests`, vignette builds disabled) completed with **0 errors, 0 warnings, 2 existing metadata/incoming notes**; outer process exit code 0. R code analysis, R-code dependencies and unstated example dependencies are all OK. Tests were run separately as described above.

CI validation on `a0e4008794cc9d1392810c8ed4690e3793b185c4`:

- **macOS, Ubuntu and Windows R-CMD-check all pass**, with package tests enabled; pkgdown also passes.
- Sparse-coercion coverage verifies lossless preservation of NA/Inf, while public integration-entry tests require NA/NaN/Inf/-Inf to fail before backend execution without mutating the input. The targeted repair run passes 23 cases and 141 assertions.
- A separate full-suite run in the local R 4.5.2 installation reports 7,320 passing assertions and 16 failures in unchanged CCC/Python/Seurat/Monocle/Presto tests. Those files match upstream/main; no changed spatial/sparse test failed. That additional local full-suite run is **not** claimed to pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06d363dad24b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.