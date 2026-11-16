# Issue

**Title:** Remove gdal/terra and add sf dependencies.

## Description

gdal is no longer used and its dependency prevents building on Ubuntu, at least, so I removed it from the DESCRIPTION file. I checked building on Ubuntu and MacOS.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b17745d949d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.