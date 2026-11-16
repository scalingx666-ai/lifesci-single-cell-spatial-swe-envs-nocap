# Issue

**Title:** [r] add examples for fragment io operations

## Description

Pretty self explanatory, with the design choice logic from  I did add some horizontal breaks as discussed from our chat, for multiple functions in the same Rd. This should help with readability going forward.

I chose to use a 500 cell dataset instead for opening frags, in consideration of download size and space.  I was thinking about doing a QC step so we could write faster, but I feel it doesn't make sense to throw the intermediate filtering in the function examples

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16faeade0a26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.