# Issue

**Title:** Fix deploy by read dist path form output of previous steep

## Description

In #291 I wrongly assume that artifacts will be available in `dist` directory (like it was in the past before I split my deploy pipeline on multiple jobs).  

This PR fix deploy by use output of previous steep documented here https://github.com/hynek/build-and-inspect-python-package?tab=readme-ov-file#outputs

It should work now.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `069c0d47ea2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.