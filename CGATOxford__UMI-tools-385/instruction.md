# Issue

**Title:** avoids keyError when generating random reads

## Description

@IanSudbery - You happy with this? The KeyError is already picked up also during the read parsing and the user will be informed at this point how many missing cell tags there were and an example read given.

I'll update the tests to cover this too before merging.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5e99b633932d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.