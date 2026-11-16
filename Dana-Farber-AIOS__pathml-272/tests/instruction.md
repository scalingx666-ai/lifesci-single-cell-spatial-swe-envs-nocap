# Issue

**Title:** Bioformats dtype bug

## Description

This is a fix for #271. Checks the pixel datatype from the OME metadata and uses that to scale the image appropriately before converting to uint8.

In my prototyping this seems to work but we need to add some tests for this

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e66a1d768415`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.