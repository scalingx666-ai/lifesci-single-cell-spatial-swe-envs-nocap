# Issue

**Title:** Moving to uv + hatch

## Description

Fixes 

I mainly moved from `tox+pip` to `hatch+uv`.
The CI's should be equivalent but I changed:
- Changed matrix to be more of an explicit list
- Used `github.workspace` instead of hardcoded path for linux runners

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10e5e443e0b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.