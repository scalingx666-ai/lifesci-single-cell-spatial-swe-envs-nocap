# Issue

**Title:** Add multiprocessing option for the MCKP estimator

## Description

So far in local testing, this is not actually faster than a for loop through chunks on a single CPU.  I do not quite understand why.  These are all in-memory CPU operations.  There are chunks of genes.  It really seems it should be the case that, if everything can be contained in memory, working on multiple chunks concurrently would be a big gain.

Input argument is `--estimator-multiple-cpu`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7d09ae753cd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.