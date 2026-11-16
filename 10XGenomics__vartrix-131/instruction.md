# Issue

**Title:** feat: Add aarch64 targets to release matrix

## Description

Add `aarch64-apple-darwin` and `aarch64-unknown-linux-gnu` to the Travis CI build matrix using native arm64 runners, and update `ci/utils.sh` to handle `aarch64` in host(), architecture(), and the new is_aarch64() helper.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3dd49885e9c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.