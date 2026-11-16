# Issue

**Title:** Docker m2

## Description

Purpose:
This PR is to update the Docker .yml file in the github workflow section.

Changes

Updated the version of the push action from 2.7.0 to 4
Added a platforms statement in the "Build and push" section to include linux/amd64,linux/arm64
Updated the environment.yml to match Sreekar's update to the Openslide version

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4b61b5f00f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.