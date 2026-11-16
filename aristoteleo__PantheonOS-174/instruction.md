# Issue

**Title:** feat(live_view): the desktop plane — five tools that drive any window

## Description

The agent could drive views it opened (live_view_*, view_id-scoped) but not windows the user opened. Five tools normalize the desktop plane: desktop_windows / desktop_open (double-click routing as a tool, app open-pipeline included) / desktop_read / desktop_update / desktop_call, riding the existing chat-stream + pending-future transport, answered by the connected Atrium via report_desktop_result. Atrium-side handlers land in pantheon-atrium.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2ec5bd08c83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.