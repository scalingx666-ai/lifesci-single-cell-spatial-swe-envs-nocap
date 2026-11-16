# Issue

**Title:** [r] fix nesting bug in `range_distance_to_nearest()`

## Description

Within the codeblock conditioned on param `AddArchRBug`, all ranges are deemed as overlaps when no ranges are actually present.  This results in all `upstream` and `downstream` values being set to 0.  
The bug occurs because `overlaps` becomes set to `integer(0)`.  When running `range[-overlaps,]`, the intended effect would be to remove 0 rows, rather than removing all rows.
I fixed this just by doing a length condition check after calculating `overlaps`.  Also added a small test for this function, for range with and without nesting.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `966820b8da47`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.