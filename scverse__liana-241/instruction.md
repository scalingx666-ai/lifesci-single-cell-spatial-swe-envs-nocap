# Issue

**Title:** Feature/mofa inflow tutorial

## Description

Add MOFA-Flex & Inflow tutorial and `lrdata_to_mudata` utility

## Summary
- Add `liana.multi.lrdata_to_mudata`, which converts an inflow-score `AnnData` (e.g. from `liana.method.inflow`) into a `MuData` object with one modality per sender cell type, ready for MOFAflex-style multi-omics factor analysis. 

- Add `docs/notebooks/inflow_mofaflex.ipynb`, a tutorial walking through running `inflow`, converting to `MuData` with `lrdata_to_mudata`, and analyzing the result with MOFAflex.

- Register the new function in `liana.multi.__init__`, `docs/api.md`, and `docs/notebooks/index.md`.

- Add tests covering `lrdata_to_mudata` in `tests/test_multi.py`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18d574b9e3b6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.