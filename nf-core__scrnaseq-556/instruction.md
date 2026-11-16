# Issue

**Title:** Fix remaining AWS test issues

## Description

Included fixes:
- The functions that check if refgenome fixes are needed now use arguments instead of accessing `params` directly
- Moved star legacy index check before conversion to `file` as otherwise does not work in combination with the fusion file system
- Remove explicit version captures for legacy index conversion modules, using the topic emit instead

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `77bfdf84017d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.