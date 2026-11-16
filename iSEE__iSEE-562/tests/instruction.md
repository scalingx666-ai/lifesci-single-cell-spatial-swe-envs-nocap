# Issue

**Title:** Fix GHA workflow for macOS

## Description

This small commit fixes the GitHub Actions workflow by adding macOS dependencies required to installing Cairo, which you need for iSEE.

Tested at

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26c71eb56efd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.