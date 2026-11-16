# Issue

**Title:** Rename private class methods

## Description

I have stumbled upon the bug described in issues #272 and #280 when using the most recent version of CheckM on macOS. It seemed to be limited to python 3.8 (while all worked as expected on 3.6 and 3.7) - a small poking around brought me to this issue:  In short, it seems there is a bug when using multiprocessing in combination with private `__methods` that was introduced in cpython somewhere around python 3.8 which leads to the `AttributeError`s described in those linked issues.

It is not clear to me whether this is going to be fixed or not on the python level and since CheckM is basically (mostly) unusable on python >=3.8 I renamed all of the private methods to only use a single underscore (_all_ of them, even if they are not used in combination with multiprocessing, for consistency). I hope that's ok - of course, feedback will be very much appreciated :)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1343a1c75d8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.