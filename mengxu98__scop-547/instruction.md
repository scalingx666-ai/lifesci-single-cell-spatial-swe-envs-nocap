# Issue

**Title:** Add gap-aware soft contours to enrichment rank plots

## Description

Add a soft decorative silhouette around dense enrichment rank point clouds, building directly on #546 (8288c84). Adjacent points are split into segments using normalized panel distances and point sizes before fitting; segments with fewer than four points remain unfilled, and large gaps are never bridged.

Smooth upper/lower visual bounds within each segment and layer translucent group-colored fills beneath the unchanged scatter points. Lighten highlighted point outlines while preserving the typography, label curves, and panel layout from #546. This is a decorative contour, not a confidence interval or a change to enrichment scores.

Validation:
- 44 targeted test assertions passed, including gap separation, ordered finite contour bounds, unchanged scores, and singleton behavior.
- Real stored MG4–MG6 enrichment results rendered and visually checked; private data are not committed.
- Scoped styler formatting and git diff --check passed.
- pkgload::load_all('.', quiet=TRUE, compile=FALSE) completed with local DLL-registration and testthat build-version warnings.
- Required R CMD check with --as-cran --no-manual --no-examples --no-tests was launched with a 120-second timeout and is not yet complete. Dependency-code/example warning checks are not yet verified.

No new dependencies, public parameters, or package-version changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b733e3ff3932`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.