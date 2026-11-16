# Issue

**Title:** Clean up max-category front-end limit

## Description

This PR implements the changes described in #2296, and reverts the regression that caused #2225.

In the case where the number of labels in a category exceeds the global "max-category-items" limit, the front-end will consolidate excess categories into a "all other labels" label.  This change simplifies the component rendering, removing the need to implement category label "truncation" at render-time.

Test snapshots changed because the `<div>` element previously containing the "truncated category" string was removed from the category component.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27575b8d867a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.