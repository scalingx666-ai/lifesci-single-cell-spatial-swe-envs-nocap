# Issue

**Title:** Clustering with re-implementation of spagcn

## Description

This pull request implements: 

- [x] reimplement the spagcn method with pytorch-geometry
- [x] use the total UMI counts per bucket (bin, cell), just like the stain image 
- [x] consider replace vanilla spagcn method with more advanced attention based graphical neural network methods

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b0552ec8a88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.