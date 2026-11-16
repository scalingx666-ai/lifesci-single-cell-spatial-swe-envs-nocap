# Issue

**Title:** fix(pl): preserve PDF plot layout

## Description

## Summary

This PR fixes PDF-export layout problems affecting Marsilea dot plots and continuous embedding plots.

With affected dependency combinations, dot-plot legends could be positioned inside the heatmap in PDF output. Continuous embedding colour bars could also shift when `axes_grid1.inset_axes` interacted with tight PDF bounding-box calculation.

## Changes

- add a direct `legendkit>=0.5.0` requirement for the Marsilea plotting stack;
- render dot plots in place and return/save their actual Matplotlib Figure;
- restore support for dot-plot titles and explicit `save=`;
- preserve the historical Figure-return contract of `rank_genes_groups_dotplot`;
- replace the continuous embedding colour bar with native `Axes.inset_axes`;
- prevent flow-layout code from manually moving native inset colour bars;
- save embedding PDFs from their owning Figure without a second tight-bbox relayout.

## Result

PDF exports now retain the expected title, legend placement, colour-bar placement, and panel geometry. PNG behaviour and existing public plotting APIs are preserved.

## Tests

- `python -m pytest tests/pl/test_dotplot.py tests/pl/test_plot_export.py -q` — 10 passed
- `python -m compileall -q omicverse/pl`
- `git diff --check`

The regression tests cover dot-plot PDF export, title and Figure handling, rank-dotplot return compatibility, and continuous-embedding PDF export without `axes_grid1.inset_axes`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2adf4143dfaa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.