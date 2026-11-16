# Issue

**Title:** Add expression-colored contours and refine dimensional density plots

## Description

`FeatureDimPlot()` can now draw expression-colored density contours without cell points using `add_density = TRUE, show_points = FALSE`. Contour geometry follows cell density, while color is the local Gaussian-weighted mean expression, including zeros. Filled expression surfaces add fine density contours and a narrow fade at low-support edges.

Improve contour readability with major/minor line widths, close `CellDimPlot()` contours by padding the plotting grid, and render filled cell density as vector bands with fine contours. Existing palette controls and legend titles remain available. The only new public argument is `show_points`, appended to preserve positional calls; no new public plotting function or dependency is introduced.

Preserve point expression values/colors, split/shared scales (including zero-expression panels), explicit fixed-color density calls, blended-feature density plots, and graph edge widths. Default unblended feature density now uses expression colors; explicitly supplying `density_color` keeps fixed-color cell-density semantics. Filled cell-density rendering changes from a raster surface to bands. Parameter documentation stays directly in the existing function source. Help examples demonstrate contour-only expression, expression surfaces, cell-density lines, and filled cell-density bands using bundled single-cell data.

Validation:
- Three focused test files passed on macOS / R 4.5.3 / ggplot2 4.0.3: 123 expression-density, 116 cell-dimension, and 32 theme assertions (271 total; no failures, warnings, or skips).
- Independent graph combinations preserved each edge's original linewidth, including nonconstant weights.
- Regenerated both help topics twice from inline documentation, confirmed stable output, and checked the Rd files. Executed all four new contour examples extracted from the generated help using 1,000 built-in single cells.
- Source package build passed. R tests used the existing local native library via `pkgload`; a fresh native compilation and full SCOP package check were not run locally.
- Rendered both functions in line and filled modes using all 1,000 cells from bundled `pancreas_sub`; all rendered line paths were finite and closed. Inspected the exported PNG and PDF. Preview colors use existing palette arguments.

The companion axis-label fix is in mengxu98/thisplot#24. SCOP does not require that fix to construct the density layers; corrected `theme_blank()` label placement requires the updated thisplot version.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0720e0a239e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.