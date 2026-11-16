# Issue

**Title:** Refactor tiles and masks with h5 management

## Description

Closes tasks 2 and 3 in #69.

Manage Tiles and Masks objects through .h5. Enormously reduces RAM overhead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dee688e807b5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.