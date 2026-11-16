# Issue

**Title:** Add Paga plot with vkey arguments

## Description

scv.pl.paga is now the scv version of paga that (if a basis is given) projects the paga graph onto the scatter plot in the embedding.
scv.tl.paga is the scv version of paga in tools that accepts vkey as an argument.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `721150414748`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.