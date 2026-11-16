# Issue

**Title:** Plot fixing

## Description

Added an argument in the call of matplotlib.pyplot to include the legend in full: 
bbox_inches='tight'

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `751613fa5635`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.