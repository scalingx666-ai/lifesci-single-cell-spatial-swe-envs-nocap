# Issue

**Title:** Switch to findDistance instead of using last=1 in findKNN.

## Description

Overlooked another change that leads to the [current build failure](https://bioconductor.org/checkResults/devel/bioc-LATEST/scDblFinder/teran2-buildsrc.html) on the BBS.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b58f807da3c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.