# Issue

**Title:** [r] Function examples for reference annotations

## Description

Pretty self explanatory, with the design choice logic from #207.  I did add some horizontal breaks as discussed from our chat, for multiple functions in the same Rd.  This should help with readability going forward.

Main thing I am iffy about is parameterization.  Is it worth it to include the additional parameters within examples, or should we just table that until CRAN release?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16faeade0a26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.