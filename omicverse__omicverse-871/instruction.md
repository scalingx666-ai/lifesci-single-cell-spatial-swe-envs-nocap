# Issue

**Title:** fix(bulk2single): repair deconvolution option forwarding

## Description

## Summary

Fixes Scaden option forwarding and marker-selection name shadowing in Bulk2Single workflows.

## Changes

- Sends scale and pseudobulk_size to Scaden instead of the unsupported scaler argument.
- Preserves the existing TAPE scaler path.
- Appends new parameters after existing arguments to preserve positional compatibility.
- Separates Scanpy module, AnnData, and expression-table variable names in marker-selection code.

## Validation

- 4 focused Bulk2Single regression tests passed.
- Tests cover Scaden options, TAPE scaling, create_st, and DFRunner marker selection.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `959c962059d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.