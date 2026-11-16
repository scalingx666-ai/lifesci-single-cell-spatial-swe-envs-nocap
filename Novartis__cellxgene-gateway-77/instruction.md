# Issue

**Title:** Filter directories without h5ad files

## Description

This change makes `scan_directory` return only h5ad files or directories containing h5ad files. 

The approach here is to add a filter in the upward traversal (leaf to root) that includes only those branches that either contain files or other branches containing files (which have already been checked). Since the h5ad file type filtering happens before, it also exludes non-empty directories without h5ad files.


![image](https://user-images.githubusercontent.com/54448967/195390194-b4a5695c-711c-427b-92b7-984a83c67f70.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `79c3f588b6b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.