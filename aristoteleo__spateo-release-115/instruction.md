# Issue

**Title:** add find_peaks function

## Description

May be useful in finding watershed markers for segmentation based on **sparse** RNA (i.e. nuclear RNA). This method performs poorly in dense regions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `19afb3403520`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.