# Issue

**Title:** Add GitHub Action for redis-cell

## Description

Start transitioning from Travis to GitHub Actions starting with adding a
new action.

Most code based on examples in the Rust Actions repository:

https://github.com/actions-rs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a47e993dcb4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.