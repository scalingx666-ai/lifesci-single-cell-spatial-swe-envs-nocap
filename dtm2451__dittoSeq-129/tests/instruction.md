# Issue

**Title:** bug-fix: dittoHeatmap shouldn't toss genes with pre-scaled (mean of 0) expression

## Description

Literal fix: actually check for non-zero values, instead of just a non-zero sum, when removing genes with zero expression.

Per #127

ToDo:
- [x] unit test
- [ ] understand Seurat's DoHeatmap methodology better so can more confidently describe how to recreate their plotting style.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ac2670cf9a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.