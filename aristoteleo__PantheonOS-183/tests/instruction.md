# Issue

**Title:** feat(desktop): the toolset learns the virtual desktops

## Description

Atrium grew mac-style virtual desktops; the agent surface catches up: desktop_windows reports active_space/space_count + per-window space, desktop_open takes space (0=current, past-the-end mints a new desktop), desktop_call gains $move_to_space. Skill updated; Atrium answers the new fields.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `89fcbceb8e60`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.