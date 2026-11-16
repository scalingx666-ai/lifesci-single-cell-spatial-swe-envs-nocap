# Issue

**Title:** fix 2 bugs in RunMixscape

## Description

This PR fixes two bugs in RunMixscape():

1. Reported by multiple users (): When the number of cells in a gRNA is less than min.cells, the function should label them as "NP" according to the documentation. But in fact they are labelled as "NT" in the "mixscape.global" column because these cells are not correctly identified.

2. Related to 1. There is a 2nd bug in RunMixscape: when it tries to check for gRNA with cells less than "min.cells", it actually checks for number of cells less than "min.de.genes" (definitely a typo). this is fixed now as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f76bd63c5010`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.