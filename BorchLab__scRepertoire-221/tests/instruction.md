# Issue

**Title:** Fix to clonalBias.R function

## Description

Storing background frequencies as list instead of DF. This prevents break cases when different samples/patients do not contain all cell types. Subtypes are stored as factors, to make sure that vector have the same length, and same order.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69c7d9dec771`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.