# Issue

**Title:** Fix #5845 raster always on VlnPlot

## Description

Hi Seurat Team,

Quick fix for #5845 which turned raster on all the time as long as the package check passed instead of if the raster conditions were met.  Just moved `raster <- TRUE` up one set of brackets.

Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e437febdcd5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.