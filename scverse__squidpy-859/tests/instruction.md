# Issue

**Title:** Add function to assign observations to a sliding window

## Description

## Description

This PR adds a new function, sliding_window, to the codebase. The sliding_window function divides a tissue slice into regularly shaped, spatially contiguous regions (windows). It allows for the analysis of spatial data by segmenting the tissue into smaller, manageable windows with optional overlap.

## How has this been tested?

PyTest on `sq.datasets.mibitof()`

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `945e127b0e69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.