# Issue

**Title:** Add calc_ntr and make an enabler for cell_cycle_score

## Description

1. create a `_calc_ntr` function and call it within the Monocle recipe.
2. Add a `cell_cycle_score_enable` parameter to allow users to enable the function.
3. Make a minor fix by removing the line that raises a NotImplementedError in the `cell_cycle_score` function, which always causes an error with the default parameter '`show`'.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9b39580733c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.