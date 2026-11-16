# Issue

**Title:** FIX: scv.tl.rank_dynamical_genes and multidimensional array

## Description

## Bug fixes

This fixes a bug in `scv.tl.rank_dynamical_genes` where an attempt to slice a pandas index using a multidimensional numpy array raises a `ValueError` as that type of operation is no longer supported.  Now, the pandas index is cast to a numpy array prior to slicing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9dffff5b887`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.