# Issue

**Title:** chore: Fix compatibility tests

## Description

## Changes
1. Dropped support for python 3.8 and 3.9
2. Added support for python 3.10 and 3.11
3. Updated python packages
4. Updated code and fixed unit tests 
5. Pinned Node ~16
6. Updated deps for `pupetteer` and `jest-pupetteer` 

-----
As for Python 3.12 - it requires updating flatbuffers in order to work which is a breaking change and doesn't work with the current dep tree - it will also require migration

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4281a8f816d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.