# Issue

**Title:** Fixed wrapper function for Seurat v5 objects

## Description

Instead of hardcoding assay names, the checks are now only performed on the `assay_oi` (defaults to the `DefaultAssay` of the object).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88ed08379c13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.