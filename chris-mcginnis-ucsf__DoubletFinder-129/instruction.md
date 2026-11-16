# Issue

**Title:** Doublets by type

## Description

Hi Dr. McGinnis, this pull request adds the feature discussed in #127 , along with docs and a unit test. Two details worth noting: 

- in a dataset with k cell types, there are (k+1) * k / 2 types of doublets, including homotypic, but so far this feature is set up in a simpler way so that it yields only k features as output. If the nearest neighbors of a cell include a doublet with cell types k1 and k2, then the counts for k1 and k2 are separately incremented.
- the names of the output columns have parameters appended just as you've done with the classification and pANN score.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `554097ba4e2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.