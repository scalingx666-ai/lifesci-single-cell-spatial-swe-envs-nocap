# Issue

**Title:** feat(desktop): fix the window you have — desktop_set and open-into-a-window

## Description

An agent with a wrong view had no verb for correcting it in place: desktop_update deep-merges (cannot remove config keys) and nothing could load a different file into an existing window — so it opened more windows. Adds desktop_set(window_id, state) and desktop_open(window_id=...), and teaches the discipline in the tool docs and the desktop skill. Atrium answers desktop.set and retargets on window_id.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4d69f0a4ea0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.