# Issue

**Title:** Ts refactor tools

## Description

@IanSudbery . Could you check over this before we merge into master.  I've removed the CGAT dependencies and moved the relevant code into Utilities.py. Setup.py now performs dependency checks based on the packages listed in required.txt.

Cheers

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `968ee3be2382`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.