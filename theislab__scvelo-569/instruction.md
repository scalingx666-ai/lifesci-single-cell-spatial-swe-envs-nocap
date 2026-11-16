# Issue

**Title:** Refactor and generalize `get_size`

## Description

## Changes

* Renames argument `layer` to `modality`.

## New

* Allows calculating counts per observation for an arbitrary modality, i.e. also from `adata.obsm`.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a668ab845f49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.