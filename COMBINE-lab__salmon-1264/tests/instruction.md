# Issue

**Title:** chore: sync master (v2.10.0) back into develop

## Description

Brings the 2.10.0 release state back to develop:
- the release merge (#1263);
- the workspace version bump to 2.10.0 (tag `v2.10.0`).

It also adds one commit that drops "The Docker image builds with Rust 1.99. (#1262)" from `docs/release-notes-2.10.0.md`, since #1262 was still open when 2.10.0 was tagged. The GitHub release notes leave it out too.

develop is an ancestor of master, so this merges without conflicts. As with 2.9.1 (#1257), use "Create a merge commit" to keep the history parallel to master.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `987c2bdced4e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.