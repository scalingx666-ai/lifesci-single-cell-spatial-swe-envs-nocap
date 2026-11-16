# Issue

**Title:** Implement group.by arg to FindAllMarkers

## Description

I saw @AlbertoFabbri93's suggestion on #4775 and thought it was a good idea. Currently, one can't group the cells for FindAllMarkers by anything besides the object's idents.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `627877914157`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.