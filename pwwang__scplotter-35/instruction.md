# Issue

**Title:** fix(FeatureStatPlot): plot features taken from meta.data for objects …

## Description

…without a dimensional reduction, where cbind(object@meta.data, NULL) failed with "arguments imply differing number of rows"

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7213705bd07b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.