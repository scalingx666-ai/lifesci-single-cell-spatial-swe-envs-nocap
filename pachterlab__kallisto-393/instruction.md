# Issue

**Title:** Added option to change d-list overhang

## Description

This branch implements the option to manually control how long the d-list overhang on either side of each unitig should be. Pass in a (>0) integer via the `--d-list-overhang` flag.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f8edbd98b52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.