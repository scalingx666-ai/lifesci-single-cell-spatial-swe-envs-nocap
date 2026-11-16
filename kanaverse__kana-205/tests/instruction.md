# Issue

**Title:** Begin improving the table for cell type labels.

## Description

- [x] Return the per-label/per-reference scores from the worker and show them in the table.
- [x] Change the parameter choices to just "use all references", or select references to be used.
- [x] Allow passing of annotations or custom selections in the cell labelling tab.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6289ab52a105`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.