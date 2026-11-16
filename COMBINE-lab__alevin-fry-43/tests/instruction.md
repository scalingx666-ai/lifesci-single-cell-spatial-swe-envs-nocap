# Issue

**Title:** [MISC]: Bump edition, remove late variable assignments, fix clippy lints, replace new objects with slices, and other.

## Description

This pr does a couple of things:
* Fix clippy listing errors
* variable declarations for `match/if` chains 
* change `String`with `&str` a few places(This should be done in more places, theoretically it might reduce execution times)
* Bump edition to 2021
@rob-p I am just wondering. Should I go ahead and bump the version number of both alevin-fry and libradicl?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1fa8e4bbe229`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.