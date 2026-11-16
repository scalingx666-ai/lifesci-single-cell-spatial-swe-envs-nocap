# Issue

**Title:** ci: auto-bump the Homebrew formula on each release

## Description

## What

Add a `release: published` workflow that opens a version-bump PR to **brewsci/homebrew-bio** whenever a stable release is published, so `brew install salmon` stays current without manual formula edits.

## Why

salmon ships prebuilt per-platform binaries via cargo-dist and is packaged in the brewsci/bio Homebrew tap. Today the tap formula is updated by hand, so it lags releases. This closes that gap automatically.

## How

`brew bump-formula-pr` (via `dawidd6/action-homebrew-bump-formula`) recomputes the per-platform `url`/`sha256` from the new release and opens the PR. It skips prereleases, and a `workflow_dispatch` input can bump an existing tag manually.

## One-time setup (maintainer)

Set a repository secret `HOMEBREW_TAP_TOKEN`: a PAT with `public_repo` scope that can fork brewsci/homebrew-bio and open a PR from the fork. Until it is set, the job is a no-op-ish failure on release (does not block the release workflow).

Companion to the formula update brewsci/homebrew-bio#2190 (salmon 2.1.1, which also adds a `livecheck` block so the version is detectable).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `724ed060db52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.