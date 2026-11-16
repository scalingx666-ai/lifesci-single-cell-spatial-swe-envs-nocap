# Issue

**Title:** Bioformats

## Description

Updated bioformats backend to support multi-level .scn images. Added  level_count and shape_list parameters. The original shape parameter was changed into the largest shape for display.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `880190661f9a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.