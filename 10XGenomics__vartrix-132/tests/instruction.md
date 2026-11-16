# Issue

**Title:** build: release on version bump; build all 4 binaries

## Description

Replaces the tag-push release workflow with one driven by `Cargo.toml`, and adds a manual build-only workflow.

## Changes
- **`build.yml`** (new): builds x86_64 and aarch64 binaries for Linux and macOS, runs a `--help` smoke test, and uploads them as workflow artifacts. Runs manually (`workflow_dispatch`) to get binaries without releasing, and is reusable (`workflow_call`).
- **`release.yml`** (rewritten): when a change to `Cargo.toml` lands on `master`, reads the version, skips if `vX.Y.Z` already exists, otherwise calls `build.yml` and runs `gh release create` with all four binaries and generated notes. The tag is only created once every build has passed. Can also be dispatched manually.

## Releasing
Bump `version` in `Cargo.toml` and `Cargo.lock` in a PR and merge it. Builds use `--locked`, so the lockfile must be committed with the bump.

## Notes
- The old Linux build used the private `toolchain-scripts` Docker image and `GH_PAT`; it now builds natively on `ubuntu-22.04` / `ubuntu-22.04-arm`.
- Pushing a `v*` tag no longer triggers a release.
- Runner labels `macos-15-intel` and `ubuntu-22.04-arm` should be confirmed as available to the org.
- Not yet run; workflows only appear in the Actions tab once on the default branch.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c34396f4c87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.