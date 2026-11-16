# Issue

**Title:** chore: sync master (v2.9.1) back into develop

## Description

Brings the 2.9.1 release state back to develop: the release merge (#1256) and the workspace version bump to 2.9.1 (tag `v2.9.1`). develop is already an ancestor of master, so this is a fast-forward with no conflicts; "Create a merge commit" keeps the history parallel to master, as for 2.9.0 (#1254).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c54dff2d62f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.