# Issue

**Title:** Fix @claude workflow: add checkout and match official config

## Description

## Summary
- Add `actions/checkout@v4` step (fixes `fatal: not a git repository` error)
- Add `actions: read` permission (allows Claude to read CI results)
- Add `pull_request_review` trigger for `@claude` in PR reviews
- Add issue title-based `@claude` trigger
- Now matches the [official example config](https://github.com/anthropics/claude-code-action/blob/main/examples/claude.yml)

## Test plan
- [ ] Merge and comment `@claude` on PR #425 to verify it works

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e1e6ee4ab56d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.