# Issue

**Title:** Ligrec Reproducibility and Bug Fix in Sparse Data.

## Description

Fixes  and 

When comparing version 1.2.4 and main, I noticed 0's were integers while non zeros were floats in the main branch while in the old version they were all the float. I think this caused some rounding problems and integer divisions. I have some ideas on how to expose these bugs on unit tests but I just wanted to open this PR to show the fix.

Ligrec needs two things but I seperated the other to simplify this PR. Normally we also need to modify numba code because it doesn't parallelize due to an assertion exitting the loop early. Those changes are in this branch: https://github.com/scverse/squidpy/compare/main...fix/ligrec

The notebooks are now reproducable by my local tests. We used notebook tests on the CI in moscot, do you think we can also do this in squidpy @timtreis ?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e44440e0855e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.