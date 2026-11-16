# Issue

**Title:** Fix `igenomes_base` issue when `igenome_ignore` is true

## Description

This should fix #568. This is how other pipelines (e.g. rnafusion) have this configuration set.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `500a69b7264c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.