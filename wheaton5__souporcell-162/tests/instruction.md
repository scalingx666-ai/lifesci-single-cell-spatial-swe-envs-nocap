# Issue

**Title:** troublet: add singlet/doublet posteriors to clusters.tsv

## Description

The log probabilities in the  `clusters.tsv` file output by `troublet` are difficult to interpret.
In particular, it is not obvious how they relate to the singlet/doublet assignments.

I've adapted `troublet` to include additional columns for `singlet_posterior` and `doublet_posterior`, which I understand are the actual values used to determine assignments. We hope to use these to better interpret `troublet`  results.

No changes have been made to the methods used to calculate `singlet_posterior` and `doublet_posterior`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b7ef0c9f4dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.