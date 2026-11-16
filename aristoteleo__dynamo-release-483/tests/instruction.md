# Issue

**Title:** fix additional issues regarding regress out

## Description

1. fix to use X_pca for pca instead of the X  in .obsm
2. fix documentations in `regress_out_chunk`
3. period after each line of documentation
4. For the n_cores, set default to be None. And then use half of available core as the default within the code.
5. timeit should be removed.
6. Do deep copy for comparison of prev and after variables.
7. Please note that there is no duplicate operation in linear regression. The function regress_out_chunk is called twice in this code because it is being used to perform two separate tasks.
      -  1st: is used to predict the effects of the variables that are being removed from the target variable y_new. 
      -  2nd: is used to predict the residuals after removing the effects of all the variables that were removed from the target variable.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b9f302a2bfe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.