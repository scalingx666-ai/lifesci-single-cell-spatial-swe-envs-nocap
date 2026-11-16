# Issue

**Title:** update to v0.42.4

## Description

- multithreaded pseudoalignment
- bias parameters and fragment length distribution integrated into HDF5 (integration now exists in sleuth)
- bug fix when read maps to the end of a transcript

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5c5ee8a45d6a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.