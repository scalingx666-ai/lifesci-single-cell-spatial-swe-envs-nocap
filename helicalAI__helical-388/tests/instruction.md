# Issue

**Title:** Main -> release 2026-07-10 (conflicts resolved)

## Description

Supersedes #386, which was unmergeable due to a `pyproject.toml` conflict.

The conflict came from the squash-merge of #383: `main`'s GH-Actions pinning commit landed on `release` as a new SHA, so re-merging `main` replayed overlapping edits from the common base. Both branches had also bumped the version independently (main: 2.1.4, release: 2.1.3).

**Resolution:** merged `origin/release` into a branch off `main`, kept `version = "2.1.4"` (higher, from main). Only conflict was the version line; everything else auto-merged. Net change into release is the #385 torch.load hardening + the version bump (the workflow/dependabot pinning is already on release via #383).

Checks were green on #386.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01dc9f12e249`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.