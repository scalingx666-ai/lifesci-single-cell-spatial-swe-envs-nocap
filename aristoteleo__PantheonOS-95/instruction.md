# Issue

**Title:** feat: gene panel selection pipeline

## Description

## Summary
Supersedes #48 with a clean commit history rebased on current main.

- Add gene panel selection pipeline with configurable algorithms (HVG, DE, RF, scGeneFit, SpaPROS)
- Runtime-configurable hyperparameters via `GenePanelConfig` and settings.json
- SpaPROS runtime gate with `notify_user` pattern for optional dependency
- Fix E2BIG kernel launch error on long sessions by stripping large env vars
- Refactor: collapse toolset into skill-scoped SKILL.md + helper scripts

## Test plan
- [ ] Run gene panel selection with default settings on a test dataset
- [ ] Verify SpaPROS graceful degradation when not installed
- [ ] Verify kernel launch works on long sessions (no E2BIG)
- [ ] Check settings.json config overrides work

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b5214ff8b83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.