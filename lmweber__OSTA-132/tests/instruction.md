# Issue

**Title:** img dimred/clustering revision

## Description

- split non-spatial/spatially aware DR into separate chapter
- hide comments, empty sections, devel code etc.
- added visuals (PCs, PCR, clusters etc.)
- make GHA ignore README changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5cfa27ab159c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.