# Issue

**Title:** Setup the auto CI/CD pipeline | Dependencies update

## Description

- Enabling auto CI/CD pipeline with results publishing. It runs only on pushed tags and need to manual signing the macOS build. Also, DockerHub secrets (user + token) need to be stored in project's secrets.
- Dependencies update

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06f08fd0b993`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.