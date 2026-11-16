# Issue

**Title:** feat: customize GroupHeatmap expression and percent legends

## Description

## Summary

`legend.position = "bottom"` moves GroupHeatmap legends but leaves the expression color bar and Percent bubbles vertical. Add `legend_params`, with separate `expression` and `percent` lists of `ComplexHeatmap::Legend()` overrides, so callers can request a horizontal color bar and a single row of bubbles.

Defaults, expression matrices, point sizes, and other annotation legends remain unchanged. Validate list names and Legend argument names, preserve the existing runtime dependency check and namespace resolver, and synchronize help and NEWS.

```r
legend.position = "bottom",
legend_params = list(
  expression = list(
    direction = "horizontal",
    legend_width = grid::unit(35, "mm"),
    title_position = "topcenter"
  ),
  percent = list(
    direction = "horizontal", nrow = 1,
    title_position = "topcenter"
  )
)
```

## Validation

Rebased onto upstream main `799930e97` on 2026-10-26; current head is `1e65f4d90968504f9318bd62402a000bd467c924`. Resolved the NEWS-only conflict by retaining both entries and the current main breaking-change section. The feature implementation, help and tests are unchanged; the PR still changes only four files.

- Source loading with `pkgload::load_all(".", quiet=TRUE, compile=FALSE)` completed. Local missing-DLL registration and testthat build-version warnings remain.
- Legend tests: 20 assertions passed; adjacent aggregation tests: 3 passed. No test failures, warnings or skips.
- Re-rendered default and horizontal legends with constructed Seurat SCT/data input; horizontal expression and single-row Percent legends visually verified. These are synthetic validation data.
- `git diff --check` passed; GitHub reports MERGEABLE/CLEAN after the update.
- Required local `rcmdcheck --no-manual --as-cran --no-examples --no-tests` with `_R_CHECK_FORCE_SUGGESTS_=false` was started; it has not completed and is not counted as passed.
- The previous head passed all four R-CMD-check jobs. Its pkgdown run finished building the site but segfaulted during R exit (139). Current main includes subsequent build-system changes; the refreshed head needs its own CI result before that failure can be considered resolved.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `799930e97b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.