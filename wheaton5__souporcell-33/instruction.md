# Issue

**Title:** switch from pyfasta to pyfaidx

## Description

avoid need for extra copies of genome & write access to genome dir:
according to the pyfasta readme: "NOTE : unless you have specific reason to use pyfasta, I suggest to use pyfaidx"

also add .gitignore.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b2bebae76af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.