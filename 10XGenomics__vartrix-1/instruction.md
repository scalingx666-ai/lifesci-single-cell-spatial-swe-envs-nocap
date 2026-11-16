# Issue

**Title:** Dev

## Description

I believe I have constructed a minimal working example. Some review of my rusty skills would be much appreciated.

TODO items:

1. Allow a user defined flag to report actual counts instead of binary values in the output matrix.
2. Write more/actual tests (right now the single test fn is basically a clone of the main fn with the test files hard-coded).
3. Make multi-threaded (although it will be worth seeing if this is even necessary, I suspect this thing will be pretty fast as-is -- the python version can get through 150k DNA variants in an hour).
4. Make sure that everything is safe and properly rusty.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbe67b9f5f95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.