# Issue

**Title:** Add Dockerfile

## Description

Add Dockerfile for docker image creation. Docker image can be built using `docker build --rm -t celltypist:1.0.0 .` from the base folder of this repository.
TBD: docker registry used to host the image

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `75d4a01e404e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.