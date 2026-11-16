# Issue

**Title:** metadata as attrs, h5 optimization through compression and chunking

## Description

More efficient storage of metadata as attrs. Add gzip compression and chunking to h5 datasets.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `68f682a0b0c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.