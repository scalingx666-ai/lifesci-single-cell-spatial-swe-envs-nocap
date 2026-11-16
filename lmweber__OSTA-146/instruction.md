# Issue

**Title:** update svg

## Description

Issue #56
- update intro
- add DESpace, HVG, and DEG (there might be some overlap with other chapters?)
- add downstream comparison (top gene examples for each method and pairwise comparison scatter plots with Pearson correlation; figures should look like below)

![plt1](https://github.com/user-attachments/assets/4720ca5d-7123-4ec6-8a49-54aaf74ac1d9)
![plt2](https://github.com/user-attachments/assets/6ad529cb-84f1-40b5-9d76-1dccd499a297)

TODO
- add references to bibliography.bib
- the commented-out nnSVG

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d490a9fe3d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.