# Issue

**Title:** feat: add compact spatial neighborhood profiles

## Description

## Summary

Add one small, read-only spatial utility: `SpatialNeighborhoodProfile()`.

- Query selected cell/spot IDs against the full resolved tissue context at multiple radii.
- Return an ordinary data frame of observed counts, totals and fractions; do not modify Seurat or store an edge table.
- Reuse `SpatialCoordinates(space = "raw")`, require explicit multi-image selection, and isolate samples with `sample.by`.
- Use a native spatial hash with fused counting; no new runtime dependencies, registry, result framework, benchmark API or automatic interpretation.
- Return shell or cumulative profiles. Exclude self by ID, keep distinct coincident cells, and report undefined composition as `NA` when total neighbors is zero.
- Add a short truthful receipt, synchronized Rd, pkgdown reference entry and a small workflow example.

```r
profile <- SpatialNeighborhoodProfile(
  spatial, group.by = "celltype", radii = c(20, 40, 80),
  cells = target_cells, sample.by = "sample_id", cumulative = TRUE
)
```

Radii use raw coordinate units, not necessarily micrometers. This summarizes observed labeled neighbors, not enrichment, significance, communication or an optimal radius. For spot assays it counts spots, not inferred cells.

## Validation

- Native package compilation and `pkgload::load_all(..., compile = FALSE)` passed.
- New focused test file: 108 assertions passed, including independent brute-force references across 10 seeds, full-context/subset equivalence, ID ordering, exact boundaries, coincident coordinates, sample separation, empty/single-cell cases, invalid input and explicit multi-image selection.
- Existing spatial-core and spatial-run-receipt tests passed.
- Rd checks and extracted example executed successfully; the added vignette chunk ran on the bundled Visium object.
- Public entry point ran on a 3,000-cell real Xenium coordinate dataset with constructed technical labels: selected results exactly matched both full-profile extraction and a brute-force reference; input object unchanged.
- Full requested `R CMD check --no-manual --as-cran --no-examples --no-tests` completed: **0 errors, 2 warnings, 4 notes**. Windows installation succeeded after moving the process-local temporary directory to the same D: volume as the dependency library; no package checks were bypassed to resolve that failure.
- The two warnings point to unchanged upstream code/documentation: undeclared `lifecycle` calls in `R/PseudobulkExpression.R` and undocumented arguments in existing plotting/integration Rd files. The new function is not named in the possible-problems or documentation diagnostics. `checking for unstated dependencies in examples ... OK` and `checking compiled code ... OK`.
- The newly installed package's exported entry point and documentation example also executed successfully from the isolated check library. The user's canonical installed library was not replaced.

GitHub Windows/macOS/Ubuntu checks and pkgdown are still running. This PR stays draft while those results are pending; local full-package check is not represented as warning-free.

Prototype performance measurements motivated the fused implementation, but are not presented as a benchmark guarantee for this public data-frame API. No claim of superiority over different spatial statistics is made.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73cee6135ce1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.