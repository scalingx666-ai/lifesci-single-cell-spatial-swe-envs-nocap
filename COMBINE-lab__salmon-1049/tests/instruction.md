# Issue

**Title:** ci: remove brewsci/bio Homebrew auto-bump (salmon is now in homebrew-core)

## Description

## Why

salmon was accepted into **homebrew-core** on 2026-07-08 (Homebrew/homebrew-core#291902, *"salmon 2.3.1 (new formula)"*). `brew install salmon` now resolves to the canonical core formula (a source build), which **Homebrew's own BrewTestBot auto-bumps** on each new release.

That makes the auto-bump workflow added in #1035 — which targeted the separate **brewsci/bio** tap — both redundant and a future liability:

- **Redundant:** the canonical formula self-bumps; the workflow did nothing for it.
- **Liability:** brewsci policy is not to duplicate homebrew-core, so the brewsci/bio salmon formula is likely to be deprecated/removed now that salmon is in core. Once that happens, `brew bump-formula-pr --tap brewsci/bio salmon` would start **failing on every release** (in an isolated job, but noisily).

## What

Removes `.github/workflows/homebrew.yml`. No other changes; homebrew-core maintains itself.

The `HOMEBREW_TAP_TOKEN` repo secret is now unused and is being removed separately; the underlying PAT should be revoked on github.com.

Reverts #1035.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01B7JMur5DmDpECddErpi2JS

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5be374914da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.