# Issue

**Title:** supportting large matrix for  the calculation of density

## Description

+ Add the `DARMA_64BIT_WORD` flag in `Makevars` to support the large data matrix in `Armadillo`.
   - if not, the calculation of density will generate error when the input data have `10 w+` `nrows` x `ncols`
+ Modify the development version since the Bioconductor 3_19 has been released.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f956c78be0b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.