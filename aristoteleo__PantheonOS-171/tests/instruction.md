# Issue

**Title:** feat(endpoint): handshake carries method signatures and docs

## Description

app_registry exposed method names only. The desktop's new per-app Interfaces view needs the callable surface: each backend method's parameters (name/annotation/default via inspect) and first docstring line now ride the handshake as \`methods_info\`, stored on the entry, exposed through describe(). Back-compatible — \`methods\` unchanged, older children simply omit the field.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6aaa87c2b7c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.