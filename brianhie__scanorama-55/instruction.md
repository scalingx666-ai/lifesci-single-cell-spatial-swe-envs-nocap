# Issue

**Title:** Add sketch-based acceleration to Scanorama API

## Description

Main improvements:
- `sketch` parameter as part of `integrate()`.
Other details:
- Added sketching reference in README.
- Removed defunct parameters in API and interpretation function.
- Added mouse brain example with sketching.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `794d08ddb697`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.