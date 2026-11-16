# Issue

**Title:** fix(desktop): desktop_call accepts the underscore spellings too

## Description

Observed in a real trajectory: three consecutive desktop_call failures with "missing 1 required positional argument: 'action'" because the model wrote `_action`/`_args`, imitating the framework's `_background`. The tool now accepts both spellings (JSON-string `_args` parsed) and returns actionable guidance instead of a signature error when no action arrives.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9391d849d226`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.