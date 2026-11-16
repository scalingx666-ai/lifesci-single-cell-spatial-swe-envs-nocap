# Issue

**Title:** Added custom latent/expression reconstruction functionality.

## Description

Added function `custom_predict` that allows you to predict the output of the model (latents and the gene expression reconstruction) with respect to only the specific covariate keys, given to the function.

* Needs further testing, debugging, and cleaning.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0cb090c4766`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.