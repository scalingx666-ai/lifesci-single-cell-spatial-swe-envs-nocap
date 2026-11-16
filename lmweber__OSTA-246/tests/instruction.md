# Issue

**Title:** Workflow: Visium HD (segmented)

## Description

- @estellad, draft of cell-level Visium HD workflow, partly based off of EuroBioC25, but simplified and using `SingleR` over deconvolution for speed.
- @lmweber this also includes the citation PR from before, to avoid merge conflicts should that be merged before.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c71cb23a68d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.