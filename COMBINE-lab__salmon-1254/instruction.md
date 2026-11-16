# Issue

**Title:** chore: sync master (v2.9.0) back into develop

## Description

Brings the 2.9.0 release state back to develop: the release merge (#1253) and the workspace version bump to 2.9.0 (tag \`v2.9.0\`).

develop is already an ancestor of master, so this is a pure fast-forward with no conflicts. Either merge method works; "Create a merge commit" keeps the history parallel to master, as in earlier releases.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1534ac8e5896`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.