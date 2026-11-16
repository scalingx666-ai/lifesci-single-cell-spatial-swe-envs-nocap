# Issue

**Title:** Updated the version of dynamo to 1.5

## Description

This pull request updates the package to version 1.5, increases the minimum required Python version to 3.9, and introduces improvements to the nullcline computation process, including progress tracking and better handling of cases where no fixed points are found.

Version and environment updates:

* Bumped the package version to 1.5 in both `setup.cfg` and `setup.py`, and updated the minimum Python requirement to 3.9 in `setup.py` and `.travis.yml`. [[1]](diffhunk://#diff-fa602a8a75dc9dcc92261bac5f533c2a85e34fcceaff63b3a3a81d9acde2fc52L2-R2) [[2]](diffhunk://#diff-60f61ab7a8d1910d86d9fda2261620314edcae5894d5aaa236b821c7256badd7L20-R20) [[3]](diffhunk://#diff-6ac3f79fc25d95cd1e3d51da53a4b21b939437392578a35ae8cd6d5366ca5485L5-R5)

Nullcline computation improvements:

* Added a progress bar to the `compute_nullclines_2d` function using `tqdm` for better user feedback during computation.
* Changed the default value of the `show_progress` parameter to `True` in the `util_topology` function to enable progress tracking by default.
* Improved robustness in `compute_nullclines` by warning and skipping the addition of fixed points if none are found along nullclines.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de553ddf8861`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.