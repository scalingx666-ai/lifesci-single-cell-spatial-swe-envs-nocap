# Issue

**Title:** Modify the SpatialMapping problem to enable solving a LinearProblem

## Description

This just checks whether `alpha=0` and in that case sets the quadratic attributes to `None`. 

Let me know what you think, I'm happy to add tests for this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e87b1a985949`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.