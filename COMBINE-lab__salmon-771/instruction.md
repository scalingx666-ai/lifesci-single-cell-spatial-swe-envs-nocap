# Issue

**Title:** minimize Docker image size by using multi-stage builds

## Description

This commit uses multi-stage builds to minimize the Docker image size.
The uncompressed size is down to 101 MB from 1.38 GB. The second 
stage of the build begins with a fresh ubuntu:18.04 image and copies in
the compiled salmon binaries. It also installs one system library that
is linked by one of the salmon shared libraries.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1cd8b22a037`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.