# Issue

**Title:** allow manual workflow triggering

## Description

This updates github Actions workflow files to enable manual triggering of workflows, so we can re-run them as needed. 
We already had this in place for the docker workflow, but now we will have it for the others as well

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9343e4e407d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.