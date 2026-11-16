# Issue

**Title:** Parent tracking

## Description

Return a list, containing a list of parent cell row indexes for each
cell.

Currently, original cells’ parents are themselves (given as their row
index in singleton list), even those identified as doublet.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5c588b41445e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.