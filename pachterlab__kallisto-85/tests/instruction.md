# Issue

**Title:** Multicore

## Description

This branch introduces multicore features to kallisto, enabling to use multiple cores for the pseudoalignment process. At the moment we don't have pseudobam integrated with multicore, so let's keep this open until we do.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `30247676e7bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.