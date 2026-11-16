# Issue

**Title:** fix(desktop): ping-handshake before the first request of a chat

## Description

A fresh chat's first desktop request races the UI's stream subscription; lost events (no replay) cost a 30s timeout each. An idempotent desktop.ping retries until the desktop answers (2s × 4), the chat is cached as ready, and the real request is sent exactly once. Atrium answers the ping in desktopControl.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5cd5622935bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.