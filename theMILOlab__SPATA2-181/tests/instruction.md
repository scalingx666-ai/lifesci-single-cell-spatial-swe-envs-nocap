# Issue

**Title:** Bug fixes | Adding plotSasDensityplot

## Description

- Fixes bug that histo image looks all black because pixel intensities were small
- Adjusts plotSasBarplot to show continuous scale on x axis (mid point of bins)
- New function: plotSasDensityplot, analogous to plotSasBarplot but showing continuous density instead of discrete bars
- Some improvements for MERFISH

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50ebc399bacd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.