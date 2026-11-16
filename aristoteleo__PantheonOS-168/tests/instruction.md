# Issue

**Title:** feat(pty): scrollback replay and pty_attach — terminals survive a desktop reload

## Description

Sessions already outlive the tab (idle reap is an hour); this adds the way back in. Sessions keep a 256KB ordered scrollback fed from the pump and the initial drain; `pty_attach(session_id, cols, rows)` rejoins a live session, replays the scrollback, touches the reaper clock, resizes best-effort; a gone session answers `{success:false}` so callers fall back to `pty_open`. Consumer is Atrium's desktop restore (terminal windows persist their session id and attach-first on reload).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f39d2bce9603`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.