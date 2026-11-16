# Issue

**Title:** feat: restyle DorotheaPlot and expand RunDorothea examples

## Description

<!-- CURSOR_AGENT_PR_BODY_BEGIN -->
`RunDorothea()` examples now show TF activity on embeddings, comparison plots follow the shared scop ggplot style, and heatmaps go through `GroupHeatmap()`.

## Changes

- **`RunDorothea()` examples** plot named TFs with `FeatureDimPlot(assay = "dorothea")` and `FeatureStatPlot()`, plus `DorotheaPlot()` bar, heatmap, dim, and target examples.
- **`DorotheaPlot()` heatmap** calls `GroupHeatmap()` on the TF-activity assay (`layer = "data"`, `lib_normalize = FALSE`).
- **Comparison plots** (`bar` / `lollipop` / `volcano`) use `theme_scop`, `palette_colors()`, and Enrichment-style colorbars.
- **New plot types** from DoRothEA / decoupleR tutorials:
  - `"dim"`: cell types + TF activity + TF expression on embeddings
  - `"stat"`: per-group activity distributions via `FeatureStatPlot()`
  - `"targets"`: regulon-target volcano (logFC vs significance, sized by `|MoR|`)
- `RunDorothea()` stores the filtered regulon table for `"targets"` plots.

## CI

- List exported `theme_scop` / `theme_spatial` in `_pkgdown.yml` so `pkgdown::build_reference_index()` can finish.
- Compare `theme_scop` to `thisplot::theme_this` with `expect_equal()` so installed-package checks pass on macOS (`identical()` fails after namespace serialization).

## Tests

`tests/testthat/test-dorothea.R`: bar/lollipop/volcano return ggplot; heatmap returns a `GroupHeatmap` list; dim/stat/targets return ggplot or patchwork.
<!-- CURSOR_AGENT_PR_BODY_END -->

<div><a href="https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503?cursor_ref=pr_footer&cursor_cta=open_in_web"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-web-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-web-light.png"><img alt="Open in Web" width="114" height="28" src="https://cursor.com/assets/images/open-in-web-dark.png"></picture></a>&nbsp;<a href="https://cursor.com/background-agent?bcId=bc-01a00f3d-19cd-7d32-b63e-ce70fd657503&cursor_ref=pr_footer&cursor_cta=open_in_cursor"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-cursor-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-cursor-light.png"><img alt="Open in Cursor" width="131" height="28" src="https://cursor.com/assets/images/open-in-cursor-dark.png"></picture></a>&nbsp;</div>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1132a755ad75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.