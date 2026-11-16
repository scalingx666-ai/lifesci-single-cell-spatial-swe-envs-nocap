# Issue

**Title:** Major refactor of single anndata eval

## Description

For single anndata inference model can now be run out-of-the-box without needing to specially download any additional files or adjust the paths

Also changed the structure of the evaluation script which essentially just does arg parsing now. Moved all functions to a new evaluate.py file

To-do: a lot of the model argument like sample size, chromosome token index etc. should ideally be inferred directly from the model without needing to be specific manually

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `22997a36d244`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.