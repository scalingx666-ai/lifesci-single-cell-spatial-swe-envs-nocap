# Issue

**Title:** Add mln example

## Description

This adds a step-by-step tutorial from preprocessing flow cell and transcriptomic reads, to pairwise alignment and segmentation, to 3D registration of serial sections.

It uses the metastatic lymph node example (downsampled version of ~50M reads each, 3 sections out of 18)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d345b7bacf67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.