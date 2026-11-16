# Issue

**Title:** Docker ci

## Description

Add a Dockerfile which builds a working environment for pathml and starts up a jupyterlab instance in the container, which users can connect to and get up and running quickly. Also add a github actions workflow to build the image and publish it to dockerhub whenever we create a new release

This will close #145

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2721cb736599`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.