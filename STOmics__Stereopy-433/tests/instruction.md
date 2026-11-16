# Issue

**Title:** update rna_velocity.py

## Description

Due to the necessity of downstream analysis, I only modified the generate_loom_with_square_bin function, so that it can retain both geneID and geneName information when creating the loom file.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `84bc719b5964`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.