# Issue

**Title:** Fix index retention in _tensor_truth function

## Description

Ensure the grts retains original index after pivoting. Currently shuffles grout truth tensor compared to activities inferred by decouple

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e1863048437`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.