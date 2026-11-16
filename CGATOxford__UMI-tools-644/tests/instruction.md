# Issue

**Title:** Update setup.py

## Description

Setup.py was still allowing install with python 2. This should force python to be at least 3 in order for setup.py to run.

I've also upped the required version of pysam. I don't know if the hack that was in place for pysam version still applies?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ce3a70a8b35`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.