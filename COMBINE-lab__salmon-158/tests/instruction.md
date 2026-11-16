# Issue

**Title:** Docker Improvements

## Description

Fixes Dockerfile to be FROM ubuntu:16.04, fixes a checksum in CMakeLists.txt, and makes build_test.sh executable.

I tested this by changing the Dockerfile to copy the code into the image rather than pulling the code directly from github so that I could test the changes I made. I then built the image and ran:
```
$ docker run combinelab/salmon:0.8.2 salmon --version
version : 0.8.2
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c0d89796fa5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.