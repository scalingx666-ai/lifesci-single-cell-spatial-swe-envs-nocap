# Issue

**Title:** expose pygam model penalties via spline_kwargs fixes #1126

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
Expose pygam model penalties via spline_kwargs. Before it was set to `penalties=["derivative", "l2"]` in the code. Now, the user can change the default by using: `spline_kwargs={'penalties':['derivative']}`

## How has this been tested?
Tested with my own data pipeline. Does not change default parameter.

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3ced63ead26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.