# Issue

**Title:** Adding <cstdint> includes to allow building with gcc13

## Description

As per https://gcc.gnu.org/gcc-13/porting_to.html, `gcc13` changes the way it handles includes. These three files needed patching to allow the build to work.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74fe0ed87897`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.