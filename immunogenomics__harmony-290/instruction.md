# Issue

**Title:** CRAN fixes

## Description

v2.0.4

Fixes issues with CRAN building (new configure script)
Conditional flag inclusion (configure script)

Fixing memory bugs (valgrind)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bad0f15852f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.