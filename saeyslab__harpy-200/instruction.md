# Issue

**Title:** Fix/kronos featurize

## Description

- hp.tb.featurize: allow writing to intermediate zarr store to reduce ram usage
- hp.io.macsima: allow specifying coordinate sytem and name of the image

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21f68d575351`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.