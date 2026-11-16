# Issue

**Title:** [r] add IterableMatrix-Methods examples

## Description

Add examples for every `IterableMatrix` method together in the `IterableMatrix-methods.Rd`.  

Using a super simple example of transforms on `as(matrix(1:25, nrow = 5), "IterableMatrix")`.  One thing that I'm thinking is it might make sense to have the examples show the result as a `dgCMatrix` instead, as the stdout doesn't necessarily show how the numbers are changed.  However, this might clutter the Rd and make it even longer than it is right now.  Any thoughts?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16faeade0a26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.