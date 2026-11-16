# Issue

**Title:** Restrict @claude to repo owner only

## Description

## Summary
- Restrict the Claude Code GitHub Action to only trigger when `vitkl` uses `@claude`
- Prevents other users from accidentally (or intentionally) spending API credits
- To add more users later, add `|| github.event.comment.user.login == 'username'` conditions

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a011793c277e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.