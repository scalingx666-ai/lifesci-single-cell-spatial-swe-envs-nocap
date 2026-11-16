# Issue

**Title:** Verbosity

## Description

Adds `verbose` parameter so user can tell doubletdetection to be silent.

Only open question is do we want some improved granularity on message presentation? Fairly straight forward to do with `logging`, but is it worthwhile, @adamgayoso?

 either way.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13710e845ee2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.