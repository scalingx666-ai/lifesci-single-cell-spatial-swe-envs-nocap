# Issue

**Title:** Set openmp conditionals for #pragma omp

## Description

* create `#ifdef _OPENMP` conditionals for #pragma omp 

Should resolve issues whereby users install pagoda2 without openmp, but use n.cores>1

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4659e00dee66`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.