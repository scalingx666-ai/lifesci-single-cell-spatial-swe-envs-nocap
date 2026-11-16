# Issue

**Title:** Fix paths in benchmarks

## Description

In #289 I have missed one constraint's path that lead to failure reported in #296

This PR fixes it and improves the report template.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13e69dfc664f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.