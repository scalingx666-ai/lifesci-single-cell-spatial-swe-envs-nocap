# Issue

**Title:** [r][cpp] Force pow to use strictly positive exponent

## Description

I realized that we shouldn't support negative exponents for powers, since that would mess up all the zero values in the matrix. Just updated a few bounds checks to make that happen

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `966820b8da47`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.