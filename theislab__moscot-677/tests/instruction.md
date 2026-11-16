# Issue

**Title:** Add Sparse Geodesic Cost Support

## Description

Here are the steps I planned. I first want to ensure the tests work with this version and I am currently on that step.
- [x] make sure it works on the new commit of ottjax (here: )
- [x] don't densify sparse arrays for geodesic costs
- [x] adjust and add tests 

In order to comply to new version:
- [x] created new solution files because loaded objects in test_regression_testing had corrupted format.
- [x] 
- [x] 
- [x] 
- [x]  (already included in this PR)
ping: @MUCDK , @giovp
- [ ]

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ba5f83919d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.