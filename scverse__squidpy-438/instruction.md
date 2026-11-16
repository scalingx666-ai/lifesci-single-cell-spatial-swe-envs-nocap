# Issue

**Title:** Fix an import for python 3.10

## Description

This should let squidpy work with python 3.10, by importing `Iterable` from the right place.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `be45fab179bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.