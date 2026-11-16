# Issue

**Title:** Debug for tutorials

## Description

Fix a few plotting bugs existing in tutorials:

- Added vectorfield parameter n to topography plot, so that we can control the number of sampling points.
- Specified networkx version and updated deprecated API.
- Fixed import error of nxviz.annotate.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dfa6a8121cd6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.