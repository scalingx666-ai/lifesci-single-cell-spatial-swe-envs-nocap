# Issue

**Title:** Github action to test pip install from branch

## Description

Add to the packaging action a test which attempts to install via 
```
pip install pytest git+https://github.com/broadinstitute/CellBender@<branch>
```
and then runs
```
cellbender -v
```
to verify the install.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d99fbdefc84`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.