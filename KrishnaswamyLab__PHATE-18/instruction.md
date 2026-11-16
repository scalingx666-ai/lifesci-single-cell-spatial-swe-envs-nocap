# Issue

**Title:** Merge from dev for pypi upload fix

## Description

Requirements for ReadTheDocs ReST and PyPi ReST are slightly different - we need two different files for these. I've also fixed github links from github.com/SmitaKrishnaswamy to link to KrishnaswamyLab instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24f12dd08b99`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.