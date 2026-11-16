# Issue

**Title:** fix(space): enable GPU defaults for cell2location

## Description

Fixes `ov.space.Deconvolution(...).deconvolution(method="cell2location")` so that GPU training arguments are passed explicitly when CUDA is available.

The cell2location scRNA reference and spatial training stages now receive `accelerator="gpu", device=1` when the user has not provided explicit device settings. User-provided `accelerator`, `device`, `devices`, or `use_gpu` settings are preserved.

Regression tests cover default GPU argument injection and preservation of explicit device arguments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58b8ca8fe481`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.