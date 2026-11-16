# Issue

**Title:** Allow `None` as `modality` in `get_modality`

## Description

## Changes

* Supports passing `None` for `modality` in `scvelo.core._anndata.py::get_modality`.

## New

* Adds a unit test to `TestGetModality` to verify using `modality=None` returns correct data.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f3c3fc62e71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.