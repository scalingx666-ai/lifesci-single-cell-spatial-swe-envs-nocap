# Issue

**Title:** Tom smith cgat patch setuptools

## Description

@IanSudbery I've hardcoded a minimum requirement for setuptools in the use_setuptools() function. previously we didn't specify a minimum version so it defaults to the latest version. 

I think this is the most likely explanation for the odd installation errors where it appears to reinstall setuptools even after installing all the requirements. This was stopping the conda build working for me. However, this also suggests the easy install solution might not work when required?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0399090a8ddb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.