# Issue

**Title:** feat(desktop): desktop_apps — the agent can see what is installed

## Description

The agent could always name an app via desktop_open(app=...), but had no way to discover which apps exist or what ids they use — so it guessed and looped. desktop_apps() returns the installed apps (id, name, description, opens, actions, backend, skill path); the desktop skill now teaches discovery first. Atrium answers desktop.apps from its registry.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d5bb15e7e81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.