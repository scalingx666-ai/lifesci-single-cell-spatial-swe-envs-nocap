# Issue

**Title:** Preserve hidden selected genes in multiselect

## Description

In `packages/view-types/feature-list/src/FeatureList.js`, the gene selection handler now preserves genes that were hidden by a filter: it recomputes newSelection to include any previously selected keys that aren’t present in the current filtered selection before calling setGeneSelection.

This ensures that multiselect keeps the filtered-out but selected genes in the shared selection state.

#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c9eb6a543ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.