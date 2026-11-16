# Issue

**Title:** Remove data.table dependency

## Description

This needs testing before merging, but I think fread and read.delim should be pretty much identical in assuming tsv. We could also look to removing after changing from bkde2d/smoothScatter to hexbin (#129)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1bd9c5e9b8d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.