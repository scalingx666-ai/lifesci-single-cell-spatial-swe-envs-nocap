# Issue

**Title:** Fix two memory use errors detected by ASAN

## Description

- SSW may return `-1` for reference alignment start coordinate (for unaligned case), causing read before buffer
 - `UniquePathLengthLowerBound` returned lambda that captured incoming argument `min_length` by reference

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3631ce0d3c14`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.