# Issue

**Title:** increase default diffexp gene count to 50

## Description

Change:  when a differential expression request is made, return top 50 results (previously, was top 10).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae23c9e5b984`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.