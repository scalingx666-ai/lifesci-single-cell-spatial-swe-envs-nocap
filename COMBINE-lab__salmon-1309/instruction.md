# Issue

**Title:** chore: sync master (v2.11.0) back into develop

## Description

Brings the 2.11.0 release state back to develop:
- the release merge (#1273), which adds the 2.11.0 release notes and the CLI reference updates;
- the workspace version bump to 2.11.0 (tag `v2.11.0`).

develop is an ancestor of master, so this merges without conflicts. As with 2.10.0 (#1264), use "Create a merge commit" to keep the history parallel to master.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c0afa6e7334`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.