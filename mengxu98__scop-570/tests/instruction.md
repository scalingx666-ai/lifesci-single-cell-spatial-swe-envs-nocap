# Issue

**Title:** feat(plot): add CellTreePlot and CIMA tutorial

## Description

## Why

Hierarchical cell annotations need a compact view of cell proportions and numeric summaries. `CellTreePlot()` draws these from a Seurat object or an annotation table.

## What changed

- Add colored sectors, branches by annotation depth, leaf tiles, proportions and optional numeric rings.
- Match counts and rings by full annotation path, retain missing values, support named colors and avoid overflow for extreme finite values.
- Add bundled PBMC QC and gene examples, plus an English CIMA tutorial with 73 subtypes and four rings.

## Scope

- One new plotting function, its regression tests, help and tutorial.
- CIMA summaries are read from the public source; no dataset is bundled.

## Blast radius

The new function uses the existing palette and theme helpers and loads ggforce when called. Existing plotting entrypoints retain their behavior.

## Verification

- Fresh package install and source package build passed.
- Cell-tree and cluster-tree tests: 158 assertions passed, zero warnings or skips.
- Rebuilt four help figures and the CIMA article; verified 73 leaf tiles, 292 aligned numeric tiles and 22 missing values, plus named colors and maximum finite values.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `25b081ffa1fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.