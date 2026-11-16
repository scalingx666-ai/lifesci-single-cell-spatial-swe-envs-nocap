# Issue

**Title:** Fix memory leak and forest classification for 2 cell types case

## Description

**Description of changes**
- Fixed memory leak in tree selection. Large datasets shouldn't run as quickly into memory overflows anymore
- Support forest classifcation metric for the case of 2 cell types #261 
- Also got rid of deprecation warnings in forest classification evaluations

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a6f76d2acef9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.