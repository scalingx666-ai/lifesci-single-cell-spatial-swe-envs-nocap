# Issue

**Title:** refactor: draw GRN network plots with thisplot::NetworkPlot

## Description

## What changed

SCENIC, SCENIC+ and scTenifoldKnk network plots now share one generic renderer, `thisplot::NetworkPlot()`, instead of each carrying its own ggplot layer code.

- `R/SCENICNetworkPlot.R`: removed the bespoke drawing path (~290 lines of `geom_segment`/`geom_curve`/`geom_point`/`geom_text` layers, the radial-label branch and the hand-built `ggnewscale` legend). `scenic_network_ggplot()` now styles the node/edge tables, calls `thisplot::NetworkPlot()`, and adds coordinate limits plus the TF legend inline.
- `R/scTenifoldKnkPlot.R`: the `plot_type = "network"` branch moved from `thisplot::GraphPlot()` to `thisplot::NetworkPlot()`, keeping status colours, KO-gene highlighting, labels and edge-width range. The user-facing theme is applied through the existing `apply_plot_theme()` helper.
- No public API change: `SCENICPlot()`/`SCENICPlusPlot()` keep their current arguments and defaults.

## Why

The old `GraphPlot` path had three user-visible problems, all visible in the comparison below:

1. numeric axes and a panel frame around the network;
2. a redundant `node_size` legend;
3. a named palette applied by factor level order instead of by name, so the legend colour did not match the node colour (legend said NS = red while the red nodes were the significant ones).

The new renderer labels every node by gene name, maps legend keys to the actual fills, and drops the redundant legends.

## Verification

- `testthat::test_local(filter = "scenic-plot")`: 132 assertions pass (covers SCENIC and SCENIC+ `network_graph`, `network` and `egrn`).
- scTenifoldKnk network plot rendered from a real `RunscTenifoldKnk()` result (that plot function has no test coverage, so this was an end-to-end run rather than a unit test).
- Rendered comparisons:

  - scTenifoldKnk, old `GraphPlot` engine vs new `NetworkPlot` engine:

    ![scTenifoldKnk comparison](https://github.com/user-attachments/assets/placeholder-scTenifoldKnk-comparison)

  - SCENIC `network_graph` and `network` on the new engine:

    ![SCENIC comparison](https://github.com/user-attachments/assets/placeholder-scenic-comparison)

  (Image links are placeholders; the renders live in the task workspace.)

## Note on dependencies

`thisplot::NetworkPlot()` is new and is **not yet released**. The `thisplot` version floor in `DESCRIPTION` is intentionally left unchanged in this PR, so hosted CI will fail on this branch until a `thisplot` release containing `NetworkPlot()` is available. Do not merge before that release lands.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0bd2c25c79e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.