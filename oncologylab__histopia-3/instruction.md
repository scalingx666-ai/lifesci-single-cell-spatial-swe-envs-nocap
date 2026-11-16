# Issue

**Title:** Expand static showcase to seven approved mice

## Description

## Summary
- allow static showcase exports to select an ordered cohort with repeated `--mouse` arguments
- deploy seven fingerprint-approved KPF atlases spanning 180 serial sections
- document cohort export and keep generated atlas assets in a checksum-verified GitHub Release

## Validation
- `pytest -q` (202 passed)
- `ruff check .`
- `ruff format --check .`
- browser-tested all seven mouse switches, K=5-15, adjacent topology pairs, desktop, and mobile
- release download SHA-256 verified: `89596ea11dd6e86d32f32f78002fce80a08acd01b11eee034e88f0c8444ec65a`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4adebf31a3ba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.