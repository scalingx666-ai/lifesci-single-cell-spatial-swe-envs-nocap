# Issue

**Title:** Fix support for "--doubletGL" argument.

## Description

Fix support for "--doubletGL" argument as described in the help. Before this patch the code would check for "--doubleGL" instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9e30aa972508`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.