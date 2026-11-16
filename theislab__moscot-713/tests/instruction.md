# Issue

**Title:** Fix: CI examples not throwing error from some commands

## Description

Here is an example case where it throws error but the CI still doesn't fail. This PR will fix that issue

![image](https://github.com/theislab/moscot/assets/32667648/7ff40ca5-32f0-4f5d-ba13-1353d843d40e)

- The script run is now a separate file
- I also added tutorials folder to the list of notebooks to execute
- added the dependencies to add the tutorials folder

It is ready for review. Once the notebooks are updated it is ready for merge imo

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1277665789ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.