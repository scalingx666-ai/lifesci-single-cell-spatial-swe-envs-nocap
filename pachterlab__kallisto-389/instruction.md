# Issue

**Title:** EM priors

## Description

This PR adds the options to supply priors to the EM algorithm. The priors are supplied as a text file to `quant` and `quant-tcc` , using the `--priors` option. The file contains line separated numbers in the same order as the transcripts used to build the index.

If the sum of the numbers in the file is greater than 1 (+ eps), we assume that raw counts are supplied instead of probabilities. In this case, we add a pseudocount to each number and then normalize them to sum to one. The pseudocount is added to prevent zero valued priors, because the EM algorithm cannot recover from that (i.e. with a zero prior, alpha will always be zero for that transcript).

However, if the sum of the numbers in the file is less than or equal to 1 (+ eps), we assume them to be probabilities and use them as is. In this case it is up to the user to ensure that no zero priors are present.

If no `--priors` file is supplied, the program will default to uniform priors as before.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b22120340fe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.