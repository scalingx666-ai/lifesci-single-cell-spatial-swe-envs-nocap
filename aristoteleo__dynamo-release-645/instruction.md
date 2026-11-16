# Issue

**Title:** Refactor `fate()` with Trajectory class

## Description

- Implement sampling methods in the `Trajectory` class.
- Replace `arclength_sampling` with `arclength_sampling_n()` since it is more robust.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5c027d53343`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.