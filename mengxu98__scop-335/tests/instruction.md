# Issue

**Title:** feat: add optional CHOIR wrapper

## Description

## Summary

- add an optional `RunCHOIR()` wrapper without making CHOIR a hard package dependency
- pin and verify the supported CHOIR backend commit (`e9ebfbc9089beeaf4ca088c7b81b18f39758b0bc`)
- add the R-only `choir` environment module to `PrepareEnv()`
- validate CHOIR results before writing clusters and trees back to the Seurat object
- reuse scop's shared scalar and Seurat-object validators instead of maintaining CHOIR-specific duplicates

This PR now contains CHOIR only. The earlier Cell2fate changes were removed during rebase because they have already landed through #336.

## Validation

- parsed all 219 files under `R/`, 124 test files, and 327 Rd files successfully
- ran 76 non-plot assertions from the changed CHOIR and external-wrapper tests successfully
- installed the real pinned CHOIR backend and verified its exact Git commit successfully
- confirmed that changed tests use internal functions directly, without `:::`
- confirmed that this PR adds no image files and no plotting tests

## Runtime note

A real 75-cell `pancreas_sub` smoke run with reduced settings did not complete within five minutes during local validation. The backend installation and provenance checks passed, but this should not be interpreted as a completed end-to-end CHOIR run; the remaining runtime is in CHOIR's CPU-heavy tree-building path.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `293301faf24e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.