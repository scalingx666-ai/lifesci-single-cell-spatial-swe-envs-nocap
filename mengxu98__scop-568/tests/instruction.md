# Issue

**Title:** fix(cnv): center heatmap colors by method

## Description

## Why

A fixed zero-centered color scale obscures inferCNV changes around its neutral value of 1. Chromosome blocks and group annotations also need to stay aligned when users customize the heatmap.

## What changed

- Show cells in rows and chromosome blocks in columns. Keep chromosome labels attached to their blocks after clustering.
- Center colors on each method's neutral value and support percentile-based and explicit display limits. Custom legend ticks can generate their own labels.
- Add a runnable CopyKAT example from public oligodendroglioma data and reuse it in both help pages.

## Scope

The changes affect CNV heatmaps, their help pages, and regression tests. CNV inference and stored scores are unchanged.

## Blast Radius

Heatmaps change orientation. Callers that rely on matrix rows or columns when composing the returned heatmap should account for the transpose.

## Verification

- Ran the CNV test suite against an installed build: 153 assertions passed.
- Built both reference pages with pkgdown and ran their CopyKAT examples on 184 cells across five groups.
- Checked that chromosome labels follow reordered blocks with ComplexHeatmap 2.8.0.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c194923d81f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.