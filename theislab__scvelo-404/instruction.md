# Issue

**Title:** Add type hints in core/_anndata.py

## Description

## New

* Type hints are added to functions in `core/_anndata.py` which did not already include any.
* Docstrings are updated by removing explicit type specifications.

## Related issues

WIP towards closing/realizing #403.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a631d724d463`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.