# Issue

**Title:** fix: honor enrichment annotation and legend border settings

## Description

Enrichment cluster strips kept visible outlines when `feature_annotation_border = FALSE`, while text-only term boxes and score legends ignored configured border colors and widths. Forward the existing feature-annotation border settings from DynamicHeatmap, FeatureHeatmap, GroupHeatmap, and NMFHeatmap, and apply the existing term border/background settings to text boxes and score legends.

Default black borders remain available. Regression tests cover custom colors and widths, independent border switches, graphical term annotations, and unchanged enrichment results.

Validation:
- 38 focused expectations passed with no failures, warnings, or skips on the current `main` baseline.
- Actual ComplexHeatmap PDF rendering confirmed gray term/legend outlines when enabled and no such outlines when disabled.
- `styler::style_file()` and `git diff --check` passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d7d9fb7976d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.