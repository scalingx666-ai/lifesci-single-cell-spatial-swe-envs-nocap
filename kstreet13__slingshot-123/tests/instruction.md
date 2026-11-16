# Issue

**Title:** Fixed ordering issue in slingCurves

## Description

Simple fix, the ordering object of a principal_curve is poorly named so the wrong order was returned.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `25fc566e9665`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.