# Issue

**Title:** Add Rcpp based implementations of selectGenes and scaleNotCenter

## Description

This adds fast Rcpp/C++ based implementations of scale() (without centering), rowMeans(), and rowVars(), and updates the functions scaleNotCenter and selectGenes to use these fast implementations. It also includes support for very large sparse matrices (greater than 2^16 elements) in these functions through 64bit integer support in Armadillo. 

Note that the necessary flag previously thought to conflict with certain BLAS routines were due to a specific MacOS configuration which was resolved with clean reinstallation of R. 

In addition, this PR introduces basic unit tests for most major functionality of the package (preprocessing, iNMF optimization, quantile alignment, some dimensionality reduction). 

Also fixes minor bugs in selectGenes and runTSNE.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9ae69817d35`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.