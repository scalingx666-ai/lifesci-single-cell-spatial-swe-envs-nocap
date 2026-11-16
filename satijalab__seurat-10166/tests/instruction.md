# Issue

**Title:** Update links to progressr intro vignette in documentation

## Description

Fix invalid link to [progressr introduction vignette](https://progressr.futureverse.org/articles/progressr-01-intro.html) in the documentation for the following functions:

- `PrepSCTFindMarkers`
- `ReadAkoya`
- `ReadNanostring`
- `ReadVitessce`
- `ReadVizgen`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74a451975f00`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.