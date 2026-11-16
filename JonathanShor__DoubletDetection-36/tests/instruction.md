# Issue

**Title:** Confidence values

## Description

Providing a p-value with p_val will have the classifier attempt to
identify clusters of cells that are boosted by synthetic doublets with
significance greater that p_val.

Overloading the cutoff return value in a non-sensical way, in
anticipation of class refactoring cleaning all this up.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3f34c256c64`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.