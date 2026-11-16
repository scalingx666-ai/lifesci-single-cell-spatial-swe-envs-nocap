# Issue

**Title:** fix bug when reading region from openslide backend at higher levels

## Description

Openslide `read_region()` uses coords in the level 0 reference frame, but pathml uses coords according to each level. This was causing a bug when extracting regions and generating tiles from the openslide backend at higher levels (#240). This should fix it by scaling the coordinates before passing them to the openslide API.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d46a37d00b06`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.