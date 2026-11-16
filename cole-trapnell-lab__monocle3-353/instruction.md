# Issue

**Title:** fix issue with library(rlist) interfering with plot_cells(..,genes=..)

## Description

fix conflict in plot_cells() when package rlist is loaded

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2e388073a17`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.