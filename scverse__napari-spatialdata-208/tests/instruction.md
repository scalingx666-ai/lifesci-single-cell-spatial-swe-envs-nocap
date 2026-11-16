# Issue

**Title:** Test spatialelement table join

## Description

Closes 

Adds a test for checking that the plot is correct even when some rows of the table are not annotating instances of the spatial element or when the spatial element contains instances not in the table.

Also, checks that this works both for the case when the `instance_key` column has dtype `int` and when it's a `str`.

Eventually, the `instance_key` column will only have dtype `int`, as discussed here:  but for the moment it would be easier if both were supported, as this PR will check.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb1f6c48811c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.