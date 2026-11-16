# Issue

**Title:** Add CLI controls for reasoning effort

## Description

## Summary
- add reasoning-effort persistence and level gating per model
- expose /reasoning command in the REPL and surface supported levels in status outputs
- remind users about effort levels after setting an OpenAI key

## Testing
- python -m compileall pantheon_cli/cli/manager/model_manager.py

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `807f307555e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.