# Issue

**Title:** Update main.rs

## Description

Updated regex for CosMx FalseCode and NegPrb to include current naming convention (SystemControl and Negative, respectively), as these weren't being filtered out correctly for new datasets. Additionally updated the pixel resolution for CosMx, which is 0.12028um/px

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf8a8ab02f34`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.