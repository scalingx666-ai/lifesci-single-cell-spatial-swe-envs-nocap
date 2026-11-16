# Issue

**Title:** Add module `datasets`

## Description

## New

* Adds module `datasets/`

## Changes

* Moves functions from `scvelo/datasets.py` to `scvelo/datasets/_datasets.py` and `scvelo/datasets/_simulate.py`
* Deprecates `scvelo.datasets.pancreatic_endocrinogenesis`

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8fae9c6804de`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.