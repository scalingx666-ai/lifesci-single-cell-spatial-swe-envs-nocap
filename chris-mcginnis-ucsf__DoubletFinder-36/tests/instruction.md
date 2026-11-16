# Issue

**Title:** Used mclapply to parallelise the parameter search

## Description

Split of part of the paramSweep_v3 code into a seperate function so that it could be sent to mclapply rather than iterating through it in a for loop. Just running on my laptop with a couple of cores it halved the run time.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba4b9782d25e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.