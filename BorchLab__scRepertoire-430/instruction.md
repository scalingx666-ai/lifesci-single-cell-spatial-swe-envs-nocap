# Issue

**Title:** Fix TRUST4 loadContigs issue in #429

## Description

This is a fix for #429 

The issue ended up being that matrix subsetting in R reduces matricies to vectors when the subsetted result will only have 1 column/row which caused an error when trying to do `colnames()<-`. Fixed this by using drop = FALSE as the k argument in matrix subsetting. This may or may not be present in other functions too - haven't checked yet.

Also did some general reformatting and refactoring but no functionality has been affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18a2d4113efc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.