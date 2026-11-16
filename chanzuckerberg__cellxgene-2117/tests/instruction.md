# Issue

**Title:** update gene set name validation to match latest requirements

## Description

gene set name validation has been updated to be more permissive.  This updates the back-end checks to match.

TL;DR on validation rules for gene set names:
* no leading or trailing white space
* no newline, return, tab or vertical tab
* no multi-space runs

This is a partial fix to #2096.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d932fb47d64`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.