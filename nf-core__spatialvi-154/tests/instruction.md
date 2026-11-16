# Issue

**Title:** Fix hard-coding of SVG method in report

## Description

This fixes an issue with the report, where the Moran's I was hard-coded, not allowing for use of Geary's C.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `441ded53109f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.