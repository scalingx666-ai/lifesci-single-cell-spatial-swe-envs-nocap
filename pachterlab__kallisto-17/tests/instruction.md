# Issue

**Title:** Bootstrap and weights fix

## Description

Create 'B' Bootstrap objects in main that run the EM algorithm. Here are the updates
- Param '-b' for the number of bootstrap iterations
- A Multinomial class that does multinomial sampling
- A bootstrap class that handles instantiation of the appropriate multinomial sampling
  - returns EMAlgorithm which you can then do whatever you want with

Fixes:
- when eff_len < 0, eff_len = len
- make TOLERANCE  smaller (will decide later what the "best" value is)

Currently serial, but will make parallel in another branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef72d3e0650f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.