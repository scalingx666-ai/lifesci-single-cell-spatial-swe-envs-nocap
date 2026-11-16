# Issue

**Title:** Docker images release job

## Description

Create a job to release docker images to dockerhub registry.

To do before merge :
- [x] Create a config variable DOCKERHUB_USERNAME with the dockerhub account username value
- [x] Create a repository secret variable DOCKERHUB_TOKEN with the token from dockerhub

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5167d2439ee7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.