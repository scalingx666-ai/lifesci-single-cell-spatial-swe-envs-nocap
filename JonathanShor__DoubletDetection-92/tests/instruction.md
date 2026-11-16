# Issue

**Title:** Fast normalize

## Description

- Stores data reused for normalization between iterations

- Still allows custom normalization method as before

- Makes p_thresh >= instead of >

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3bfa15cd27f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.