# Issue

**Title:** Add registration QC showcase and slide controls

## Description

## Summary
- add previous/next section navigation with visible-section camera fitting
- add select-all and deselect-all controls
- add a static registration QC portal for masks, section order, and histology-only 3D registration
- deploy the cleaned seven-mouse approved showcase and exclude avoided demo specimens

## Validation
- 209 pytest tests
- Ruff check and format verification
- desktop and mobile Playwright checks for atlas and QC portal
- release archive path/symlink scan and SHA-256 verification

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5c364cc62e87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.