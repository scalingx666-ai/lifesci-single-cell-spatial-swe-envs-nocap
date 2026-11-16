# Issue

**Title:** Warning message for reference SCT model counts correction

## Description

Adding a warning message so that users know if they use a reference SCT model we will hard set do.correct.umi to FALSE. We do this since count correction across models is not statistically sound, but we will send a message so that users know their counts will not be corrected. 

<!--
Thanks for your interest in contributing! 

Please refer the contributor's guide for instructions on submitting a pull request:
https://github.com/satijalab/seurat/wiki#contributors-guide
-->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26e19946d389`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.