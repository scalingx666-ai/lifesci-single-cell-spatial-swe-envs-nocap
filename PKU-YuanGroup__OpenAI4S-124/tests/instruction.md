# Issue

**Title:** ci(release): add a pypi_only dispatch mode for an already-public release

## Description

## Summary

v0.2.0 was published on GitHub before `release.yml` ever ran, so PyPI still only has 0.1.0 — and the guard's draft requirement (correct for the staging path) makes the pipeline unusable for exactly this gap: it refuses a public tag because staging assets onto one is the half-published state it exists to prevent.

This adds a `pypi_only` dispatch mode that inverts only that check:

- guard requires the tag to be **public** (a draft must take the normal publish path); `publish` and `pypi_only` are mutually exclusive; the prerelease refusal is shared.
- `attach` and `finalize` stay publish-only — nothing is staged onto the release, nothing is flipped.
- The `pypi` job replaces its implicit `success()` with explicit status functions: any needs failure still blocks it via `!failure()`, and `attach` must be `success` (publish) or exactly `skipped` (pypi_only). With `publish` set the condition reduces to the previous behavior.
- The wheel/sdist still come from the frozen tag SHA through quality, build, and every platform check, exactly as in a full publish. Trusted publishing (workflow + `pypi` environment) is unchanged.

After merging: dispatch `release.yml` with `tag=v0.2.0`, `pypi_only=true` to publish 0.2.0 to PyPI.

## Verification

Ran: YAML parse of the edited workflow (inputs resolve to tag/publish/pypi_only); the workflows README pair documents the new mode. Not run: the workflow itself — it requires a dispatch, which happens post-merge; the first dispatch against v0.2.0 is the live verification.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f3217696cea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.