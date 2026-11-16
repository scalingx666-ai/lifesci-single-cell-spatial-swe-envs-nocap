# Issue

**Title:** add arguments to asSPATA()/Seurat

## Description

Minor change which allows custom names of Seurat slots for the asSPATA function, besides "counts" and "scale.data"

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd70962a2f0c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.