# Issue

**Title:** Change niche flavor to cellcharter_simple and default distance = 3

## Description

## Description
- Change `flavor` option in `calculate_niche to `cellcharter_simple` for CellCharter
- Default `distance = 3` for `cellcharter_simple`. 

## How has this been tested?
`pytest` runs successfully. 
However, I see there are no unit tests for `calculate_niche` with `cellcharter` (now `cellcharter_simple`).

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c32e7fd16440`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.