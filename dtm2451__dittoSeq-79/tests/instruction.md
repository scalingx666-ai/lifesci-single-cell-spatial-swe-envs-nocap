# Issue

**Title:** Show all 'other' cells in background of scatter plot facets

## Description

By ensuring Others_data becomes a repeat of all_data for every facet.

To Do:

- [x] decide if should add `split.show.all.others` input for turning off this new behavior. (Seems useful situationally in conjunction with `cells.use`!)
- [x]  If yes:
    - [x] add docs
    - [x] add a test

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea1255a0901d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.