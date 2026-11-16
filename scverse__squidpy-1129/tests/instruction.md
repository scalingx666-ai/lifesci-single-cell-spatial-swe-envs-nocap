# Issue

**Title:** ci: pin virtualenv<21 to fix hatch incompatibility

## Description

## Summary
- virtualenv 21.0 removed `propose_interpreters` from `virtualenv.discovery.builtin`, breaking hatch's environment checks ()
- Adds `.github/uv-constraints.txt` with `virtualenv<21` and sets `UV_CONSTRAINT` in both `test.yaml` and `test-notebooks.yaml`
- TODO comments mark these for removal once hatch releases a fix

## Test plan
- CI should pass on this PR (the constraint file is checked out before any `uvx hatch` calls)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6dc2a91e6ee3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.