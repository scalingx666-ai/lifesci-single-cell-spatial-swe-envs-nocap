# Issue

**Title:** [r] Fix Rcpp warning about out-of-bounds access

## Description

Rcpp started warning about out-of-bounds access stating `subscript out of bounds (index 0 >= vector size 0)` on some tests. This was due to length-zero arrays in BPCells matrices arising from e.g. single element arrays with perfectly compressed data arrays (0 bits per element in the bitpacking data array).

Now we avoid accessing an index of a possibly-empty array and use an alternate method to get a data pointer.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de87d456900c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.