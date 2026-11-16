# Issue

**Title:** [python] Change runtime version mismatch check to warning

## Description

**Issue and/or context:** Towards SOMA-720

**Changes:**
Relax runtime error for mismatched build/runtime TileDB library to a warning.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41b04f22c706`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.