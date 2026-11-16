# Issue

**Title:** adds distance-based knee method and makes default

## Description

This PR adds a new method to detect the knee, based on [this stackoverflow post](https://stackoverflow.com/questions/2018178/finding-the-best-trade-off-point-on-a-curve)

The idea is to form a straight line between the first and last point on a cumulative frequency curve and then find the point on the curve which is the maximum distance from the straight line. I've introduced one tweak which is the addition of an iterate step which reduces the number of CBs included in the knee detection until the knee point detected becomes stable. Otherwise, the more reads are parsed, the more the knee threshold over-estimates the true knee position. 

This method is now the default behaviour in `umi_tools whitelist`, although the old method is still available via `--knee-method=density`. The documentation and tests have also been updated to reflect this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e1be5a2e7059`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.