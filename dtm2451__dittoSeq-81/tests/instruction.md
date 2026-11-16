# Issue

**Title:** Vignette-fix

## Description

With the current version of Seurat loaded in the BBS (Bioconductor build system), there seems to be a bug surfacing in the Seurat code chunk previously used for single-cell data prep.  This PR swaps that out for Bioconductor packages.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21c506b83f91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.