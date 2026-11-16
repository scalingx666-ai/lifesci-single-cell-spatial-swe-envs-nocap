# Issue

**Title:** Minor documentation fixes

## Description

- Use the right channel order for cellpose in the "Comparing segmentations" tuto (fixes )
- Use `#FFFFFF` instead of `#fff` for colors in the tutorials (spatialdata-plot now throws an error for `#fff`)
- Also a minor threshold update in the tests that were sometimes randomly failing due to randomness and a too high threshold

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b19079932f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.