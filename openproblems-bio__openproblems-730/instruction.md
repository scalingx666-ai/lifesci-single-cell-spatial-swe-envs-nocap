# Issue

**Title:** Check for nf rate limiting

## Description

This PR separates the preparation to run the benchmark from actually running the benchmark, and protects from NF Tower ratelimiting.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd4260a79046`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.