# Issue

**Title:** Fix for `get_feat_suffix()`

## Description

Function `get_feat_suffix()` run before checking if feature names and feature ids are different in the assays. 

Run `get_feat_suffix()` only when feature names and feature ids are same.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31fe77208ba7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.