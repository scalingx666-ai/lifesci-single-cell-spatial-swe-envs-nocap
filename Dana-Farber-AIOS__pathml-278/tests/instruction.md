# Issue

**Title:** Bioformats xy ij

## Description

Update BioFormatsBackend to use i,j coordinates (#276). Also adds a section in the docs for developers to clarify. Also registers the pytest mark to silence warning when running tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2eca9ed02e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.