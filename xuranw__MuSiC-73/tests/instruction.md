# Issue

**Title:** Prop_comp_multi/Abs_diff_multi: Fix text annotation

## Description

Without these fixes, `Prop_comp_multi` and `Abs_diff_multi` throw the following error:

> ```
> Error: Aesthetics must be either length 1 or the same as the data (9): `label`
> ```

(see issue #52).

The solution for `Prop_comp_multi` (see 0da621caf044b10fc2b53538261ea3ade4c37984) was suggested by @mxcai .
The adjustments to `Abs_diff_multi` (see e4f72c96bbff1fb2d9c67153c4084698e45c538b) were added by me but are conceptually based on @mxcai's work.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `963d32474b93`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.