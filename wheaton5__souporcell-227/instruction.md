# Issue

**Title:** Fix Singularity Definition File Error & Update the README File

## Description

This pull request includes two updates:

1. Singularity Definition File: Resolved an installation issue with PyStan by determining the Python to be 3.10 version.
2. README File:
     .  FreeBayes Command: Modified the FreeBayes usage command from using --max-coverage 100000 to --limit-coverage         100000.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af738b98ac6e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.