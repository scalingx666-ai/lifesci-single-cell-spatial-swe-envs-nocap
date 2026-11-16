# Issue

**Title:** Cells with 3 TCR chains (2alpha1beta, 2beta1alpha)

## Description

Here is a chunk of code that would deal with the cells that have more than 2 TCR chains (in case they have 2 alpha 1 beta or vice versa) so that those cells would not be discarded from the subsequent analysis (https://www.jimmunol.org/content/202/3/637)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4cacb80a55e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.