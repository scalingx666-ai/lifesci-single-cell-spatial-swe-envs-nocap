# Issue

**Title:** Read and write, h5path

## Description

Introduce a read function which checks file extension and loads with appropriate backend.

Introduce h5path, a h5 file format to store SlideData objects. Read and write functions for h5path are provided.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5856d8039ac8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.