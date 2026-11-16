# Issue

**Title:** [fix] Cellpose 4.2 compatibility

## Description

As discussed in #259, `invert` got removed as argument to `model.eval` in cellpose v4.2+, making harpy incompatible with the latest cellpose versions. 

The `cellpose_callable` function documents now handles `invert` in a version-specific manner:
- it documents the changed behavior
- For cellpose versions greater than 4.2, it raises an error when `invert=True`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df61db96a958`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.