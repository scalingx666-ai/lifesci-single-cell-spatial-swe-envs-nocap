# Issue

**Title:** Fix Cellpose gpu use during segmentation

## Description

e1979d1 (v2.2.11) drop `gpu` option in the `load_cellpose_model`, so gpu is no longer passed to Cellpose, #450.
`load_cellpose_model` now takes `gpu: bool = False` again and passes it to CellposeModel / Cellpose.

The download command is unchanged, so it stays on CPU.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41aa901f1095`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.