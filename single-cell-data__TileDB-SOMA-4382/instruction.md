# Issue

**Title:** [python] Pin pandas to be less than 3.0.0

## Description

Add a temporary pin until we can fix test failures using `pandas==3.0.0` (see SOMA-826).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a464795d6519`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.