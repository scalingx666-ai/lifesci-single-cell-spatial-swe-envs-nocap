# Issue

**Title:** Fix publish pipeline permissions

## Description

## Summary
- Add `contents: read` permission to the publish job — the checkout step was failing with "repository not found" because specifying only `id-token: write` denied the default `contents: read`
- Expand Python test matrix in both CI and publish workflows to include 3.13 and 3.14

## Test plan
- [x] Re-tag v0.2.0 and verify the publish workflow passes checkout
- [x] Confirm tests run across all four Python versions

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1f492ff4b42`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.