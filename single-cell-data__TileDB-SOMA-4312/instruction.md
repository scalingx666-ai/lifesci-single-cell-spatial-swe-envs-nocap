# Issue

**Title:** [python] Improve docstring for `from_anndata`

## Description

**Issue and/or context:** [SOMA-633]

**Changes:** Improved `from_anndata` docstring documentation for better ReadTheDocs rendering and consistency with `from_h5ad`.

**Notes for Reviewer:** Attempted to reduce duplication with `from_h5ad` where possible.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b809a2b1a0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.