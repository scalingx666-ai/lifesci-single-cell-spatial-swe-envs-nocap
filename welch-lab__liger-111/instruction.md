# Issue

**Title:** Added a parameter to selectGenes

## Description

Seems unnecessarily difficult to set the value of var.thresh for each dataset. I've added a parameter for 'how many genes do you want to find from each dataset'. It then optimises the value of var.thresh.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `622f23a088ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.