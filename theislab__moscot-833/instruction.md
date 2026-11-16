# Issue

**Title:** Fix jax version and neural

## Description

Addressing #832.
I added a requirement for the jax version to be >=0.6.1. If I understand correctly, this does not fix #830 though since the error appears when installing moscot with pip. So I think the error will still occur in the pip-downloaded version until the next release.

I moved all the requirements for moscot neural into the core dependencies to make their import not optional anymore.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a7b69d616e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.