# Issue

**Title:** Support table as input for checkm bins

## Description

When we assembled a very large number of MAGs from multiple samples with multiple binners, these MAGs were stored in different directories. If we wanted to run checkm at one time, we had to link these MAGs to one directory. 

Request support for table as input to checkm, so we only need to provide a table with 2 or 3 columns (genes) to run checkm.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c27394be435`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.