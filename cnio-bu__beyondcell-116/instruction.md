# Issue

**Title:** Update beyondcell collections

## Description

- Replace SSc with coding-only signatures
- Trim PSc and DSS to contain 250 up and 250 down genes
- Update drugInfo accordingly

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a83c4b6f3a45`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.