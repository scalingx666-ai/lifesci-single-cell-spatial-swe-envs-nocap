# Issue

**Title:** fix(space): sync cell2location one-hot handling

## Description

## Summary

- sync the vendored cell2location one-hot compatibility fix from BayraktarLab/cell2location#418
- squeeze column-shaped categorical indices before one-hot encoding and cast encoded values to float
- remove reliance on the removed private `scvi.nn._utils.one_hot` API
- cover spatial, reference, and FCLayers paths with focused regression tests

## Root cause

scvi-tools 1.4 exposes `torch.nn.functional.one_hot` directly. It returns integer tensors and preserves the trailing singleton dimension of `(N, 1)` category indices. The vendored cell2location code therefore first fails with `long != float`; casting without squeezing then broadcasts model parameters to `(N, N, genes)` and triggers the reported Pyro log-prob shape error.

## Validation

- `3 passed`: `tests/space/test_cell2location_one_hot_compat.py`
- `17 passed`: DecontX batch, font fallback, TCGA clinical, SUDE, and existing cell2location orchestration tests
- real clean Python 3.12 environment with scvi-tools 1.4.3, Pyro 1.9.1, and Torch 2.13.0: FCLayers and spatial model trace passed with `(4, 3)` float outputs
- Ruff passed
- `git diff --check` passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16f3d8f20f3c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.