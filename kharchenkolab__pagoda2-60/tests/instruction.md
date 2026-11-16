# Issue

**Title:** Update Makevars

## Description

Fix the make instructions to use the C++ compiler that is used by R for the other cpp files and specified in the .R\Makevars. 
This fixes the fopenmp issue for Macs with the clang++ 4.0 installed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `630c84ba1cc6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.