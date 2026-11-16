# Issue

**Title:** Update clonalQuant.R

## Description

This fix prevents clonalQuant from crashing when `scale=F` and `group.by` are used together. The deleted line was reassigning `x` to the `group.by` variable which is NULL when no grouping is used. `x` is correctly defined in lines 26-33.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7011982d62e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.