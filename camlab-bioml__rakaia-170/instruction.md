# Issue

**Title:** Dev (0.31.0)

## Description

## [0.31.0] - 2026-04-28

### Changed

- Use image blend and mask fill cache to cache layers for faster blending
- More informative tooltips for hover template options for performance. 
- Add `.obs` export for CosMX preprocessing example

### Fixed

- Mask boundary recompute on gating to match gate selection.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0c3a23560a64`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.