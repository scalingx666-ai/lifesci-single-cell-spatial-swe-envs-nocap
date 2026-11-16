# Issue

**Title:** fix(pp): filter unsupported RAPIDS UMAP options

## Description

## Summary

Prevents OmicVerse dispatcher options from reaching RAPIDS SingleCell UMAP.

## Changes

- Removes unsupported gamma and dispatcher-only method options from RAPIDS UMAP calls.
- Preserves gamma for the OmicVerse GPU UMAP fallback.
- Removes the conflicting dispatcher method before fallback execution.

## Validation

- 2 RAPIDS dispatch and fallback regression tests passed.
- Tests use a fake RAPIDS backend because CUDA and RAPIDS are not available locally.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3777a62fb8a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.