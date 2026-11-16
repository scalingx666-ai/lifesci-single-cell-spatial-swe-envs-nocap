# Issue

**Title:** ci(store-sync-review): invoke via 'python -m pantheon'

## Description

The agent image doesn't put the `pantheon` console-script on PATH; invoke via `python -m pantheon store ...` (validated: workflow ran end-to-end on staging).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5bf48466a339`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.