# Issue

**Title:** Switch to iSEE docker image to provide the necessary dependencies.

## Description

Split off DockerHub publication from check workflow.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31c8f8b6cd8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.