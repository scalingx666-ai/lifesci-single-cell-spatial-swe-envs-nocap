# Issue

**Title:** Fix computation of when learning should be retried with lower learning rate.

## Description

Hi @sjfleming ,

The code I added to implement --final-elbo-fail-fraction and --epoch-elbo-fail-fraction didn't really make sense before.  Now the percentage change is computed by comparing to (best_test_ELBO - first_train_ELBO) and (previous_test_ELBO - first_train_ELBO), respectively.  Basically, is there a big percentage change relative to the range of the ELBO plot.

In addition, I believe because miniconda is now python 3.8, I needed to add a version requirement for pytorch in order to not get an error.

Regards, Alec

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2507742203a3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.