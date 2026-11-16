# Issue

**Title:** fix(endpoint): methods_info actually reaches app_registry

## Description

#171 landed the handshake and the storage assignment but dropped the AppEntry field + describe() emission — methods_info was stored and then omitted from every app_registry answer. Two lines.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81b53594783e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.