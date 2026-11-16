# Issue

**Title:** chore: fix spatialdata access in squidpy via a helper function

## Description

Fixes   and implements the table extraction in a decorator so we won't need to ctrl+f our way to fix a similar bug when it happens

update: decided not to use a decorator as it uses metaprogramming with little to no benefit over using a function. Only plus was not adding `table_key` to the signature which isn't a plus imo. Explicitly typing a signature of a function is not something I consider as duplicate code

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af1b3a30125e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.