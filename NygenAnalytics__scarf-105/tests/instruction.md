# Issue

**Title:** Use thread pool executor

## Description

ThreadPool uses semlock which causes an error when using AWS Lambda

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18d8c516edb3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.