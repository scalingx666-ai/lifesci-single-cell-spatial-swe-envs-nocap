# Issue

**Title:** Simplify the tiling QC re-run stitch hint

## Description

`assign_stitch_groups` now stores its arguments under `uns["tiling_stitch"]["params"]`, so the re-run hint in `calculate_tiling_qc` prints them as is. This drops `_STITCH_PARAM_KEYS`, `_STITCH_COLUMNS` and the private imports into `_tiling_qc`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69a3beaabbc9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.