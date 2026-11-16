# Issue

**Title:** Debug arclength_sampling

## Description

`arclength_sampling` uniformly samples data points on an arc curve that is generated from vector field predictions. However, it may terminate earlier than expected, resulting in inconsistent shapes in the output.

Proposed solution: When the length of output is smaller than expected, calculate a new point with the last set of parameters.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `153f5b7c84b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.