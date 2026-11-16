# Issue

**Title:** fix: use `current_point` instead of `displayed` to fix contrast calculation

## Description

It looks like I did not focus enough on #276 and accidentally left `displayed` instead `current_point` in the code. 
It works, when I open PR as image on which I worked was loaded as RGB. Now it is loaded as 3 channels and the current code ends with an exception.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c1383034478`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.