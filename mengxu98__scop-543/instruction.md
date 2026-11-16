# Issue

**Title:** Align coverage dependency install with R-CMD-check

## Description

The weekly test-coverage workflow fails while resolving dependencies because it installs all Suggests, including GitHub-only packages (monocle3, SeuratData) that are not listed in Remotes. R-CMD-check avoids this by installing hard dependencies plus an explicit set of test packages.

This change makes the coverage workflow install dependencies the same way as the main R-CMD-check matrix: `dependencies: '"hard"'` with the same extra packages, keeping covr in place of rcmdcheck. No other workflow steps change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `216ce834556e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.