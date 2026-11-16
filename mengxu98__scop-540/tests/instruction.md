# Issue

**Title:** Add rank plots for stored enrichment results

## Description

## Summary
Add `EnrichmentPlot(plot_type = "rank")` for comparing stored ORA results across groups without rerunning enrichment. Terms are filtered through the existing enrichment selection logic and ranked by `FoldEnrichment` (or `rank_by`).

Each group uses the default Chinese palette, solid points sized by -log10(adjusted P), and black labels with a white halo and thin, arrow-free connectors. The default point-size range is `c(2, 5)`, with up to 80 terms and five labels per group. Expose point sizes/opacity, label selection/size, and shared or independent y scales. Existing plot modes retain their defaults; new arguments are appended for positional compatibility.

Rank plots accept one database per call, preserve original P values, handle zero adjusted P values for display, and return plotted data for inspection. Add generated documentation, an executable result-only example, NEWS, and regression coverage.

## Validation
- `pkgload::load_all(".", quiet=TRUE, compile=FALSE)` completed; local DLL-registration and testthat build-version warnings were emitted.
- 31 targeted test assertions passed with no test failures, warnings, or skips.
- Generated Rd parsed successfully; the new result-only example rendered successfully.
- Real stored enrichment results rendered successfully: 8 terms in the first group and 80 in each of five other groups; private analysis data are not included.
- `git diff --check` passed.
- Required `--as-cran --no-manual --no-examples --no-tests` check was invoked but remains in the early check stage; not reported as passed. An additional ordinary R CMD check is running. Dependency-code/example check results are not yet available.

No dependency, package-version, or analysis-result changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce3b500d73a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.