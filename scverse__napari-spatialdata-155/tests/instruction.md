# Issue

**Title:** Refactor duplicate logic

## Description

Currently, on main there is a lot of duplicated code. This PR provides a refactor to remove duplicated logic in `_sdata_widgets` and `Interactive`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1eb04d03628a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.