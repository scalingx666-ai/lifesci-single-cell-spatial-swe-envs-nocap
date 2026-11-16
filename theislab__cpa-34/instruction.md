# Issue

**Title:** Install CPA dependencies fixed

## Description

Torchaudio installation version was not compatible with torch/torch-lightning. Fixed.
Version --> 0.8.4

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c63d5cf5cfc7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.