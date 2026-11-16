# Issue

**Title:** fix: default SCENIC network graphs to FR layout

## Description

`SCENICPlot(..., plot_type = "network_graph")` now uses the weighted FR layout when `network_layout` is omitted or set to `"auto"`, matching the tested five-TF example. Explicit `"kk"` remains available. The default still displays the full selected network (`network_display_targets = Inf`); node and edge selection are unchanged.

Validation: the new public-API regression test fails with the old default and passes after this change; the complete SCENIC plotting test file, Rd checks, and local SCENICPlot reference-page build pass. Replaying the supplied customer edge table confirms identical coordinates to explicit FR and preserves all 463 selected nodes and 574 edges. The original customer Seurat object was unavailable for a fresh installed-package rerun.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c364fa0e53d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.