# Issue

**Title:** chore(security): add 7-day cooldown to Dependabot config

## Description

## What

Adds a **7-day dependency cooldown** to this repo's Dependabot config, so newly published package versions are not proposed until they have been available for 7 days. This gives freshly published (possibly malicious or unstable) releases time to be vetted.

## Why

Bastion auto-analysis flagged a missing cooldown (CWE-829: Inclusion of Functionality from Untrusted Control Sphere, HIGH). Security updates are **not** affected by the cooldown.

Refs helicalAI/dashboard#1154

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01HnPY71ZEkRpQWSvstkSaP1

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7ccc0ddd9e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.