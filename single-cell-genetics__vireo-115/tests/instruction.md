# Issue

**Title:** Bug in the output file prob_doublet.tsv.gz

## Description

The header line of the "prob_doublet.tsv.gz" output file incorrectly double the number of donor pairs compared with the number of actual probabilities in subsequent lines. The bug is due to the use of `itertools.permutations` instead of `itertools.combinations` when creating the header line.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97971e37a7bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.