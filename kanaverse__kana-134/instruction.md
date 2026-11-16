# Issue

**Title:** Added UI elements for subsetting on column annotations.

## Description

- Had to use a table hack to get numeric inputs to sit on the same line.
- Stored `subset` information in `tmpInputFiles[0]` for the time being, to be consistent with `batch`. But maybe it should live in the parameters object instead; it doesn't make a lot of sense to be tied to the first input object.
- Probably should add a little warning when max < min. This is difficult to enforce inside the inputs as it attempts to validate each keystroke, so you can't clear the object and start typing a new number without prematurely hitting the constraint. (Sliders don't work if the min or max value is +/- Inf, and also it's hard to get the appropriate precision.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a710f701792`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.