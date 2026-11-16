# Issue

**Title:** Don't crash with ZeroDivisionError if initial test ELBO is the best test ELBO

## Description

The --final-elbo-fail-fraction test checks that the final test ELBO isn't much worse than the best test ELBO.  It checks the (distance between final test ELBO and best test ELBO)/(distance between initial test ELBO and best test ELBO).  

This causes a ZeroDivisionError if best test ELBO == initial test ELBO.  

Solution:
If --final-elbo-fail-fraction is enabled  && final test ELBO < best test ELBO  && initial test ELBO == best test ELBO
then training is considered to have failed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `72e6a3fa405c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.