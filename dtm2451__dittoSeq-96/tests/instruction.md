# Issue

**Title:** Bug Fix: Allow `dittoHeatmap()` to properly `drop_levels` of annotations by adjusting color-picking.

## Description

Addresses #95

Note: Users will need to adjust this input deliberately when they want levels to be dropped.  The default for `drop_levels` in `dittoHeatmap()` will be set to FALSE.  This is contrary to the `pheatmap()` function itself, but should allow for consistency both 1) across plots when users might make a bunch of plots at once while not realizing that say "conditionX is the only condition without any samples from groupB", as well as 2) with previous dittoSeq outputs.

Still to do:
- [x] add unit test
- [ ] prep NEWS update for after merge

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `899049874861`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.