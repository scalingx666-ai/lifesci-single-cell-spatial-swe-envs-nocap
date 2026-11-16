# Issue

**Title:** Drop macos-x86_64 from release binary matrix

## Description

## Summary

`macos-13` on GitHub's shared runner pool has been persistently queued — the v2.1.0-beta.1 dry-run (run 24599969886) sat at 5+ hours for the `Build macos-x86_64` job before being cancelled. Every other job in the dry-run completed successfully in under 2 minutes, so this single runner pool is the sole blocker on Beta 1.

Drop Intel macOS from the release binary matrix. Intel Mac users can still install via:
- `cargo install trim-galore` (local build from crates.io)
- Docker `ghcr.io/felixkrueger/trimgalore` (multi-arch manifest covers `linux/amd64`)

Apple Silicon macOS remains covered by the existing `macos-latest` runner.

## Changes

- `.github/workflows/release.yml`: remove `macos-x86_64` matrix row from `build-binaries`.
- `README.md`: update "Prebuilt binaries" platform list and note Intel Mac install paths.

## Test plan

- [ ] Re-dispatch release workflow with `dry_run: true` on `optimus_prime` after merge; confirm all jobs reach terminal state within ~20 min.
- [ ] Confirm `Build macos-aarch64` still runs and passes.
- [ ] Confirm `create-tag-and-release` + `upload-binaries` + `publish-crate` jobs resolve correctly (skipped on dry-run, run on real dispatch).

## Follow-up (not this PR)

If Intel Mac pre-built binaries become important again, options are (a) cross-compile `x86_64-apple-darwin` on `macos-14` with Rosetta-based smoke test, or (b) paid `macos-13-xlarge` runners. Revisit post-GA if users report friction.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5447edbe139c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.