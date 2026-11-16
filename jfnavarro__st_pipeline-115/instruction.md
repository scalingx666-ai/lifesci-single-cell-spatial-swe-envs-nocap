# Issue

**Title:** Use pip instead of poetry

## Description

Removed poetry from Dockerfile. Also updated the base image to `python:3.11.14-slim-bookworm` as I was getting warnings about the previous image.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2617af793b78`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.