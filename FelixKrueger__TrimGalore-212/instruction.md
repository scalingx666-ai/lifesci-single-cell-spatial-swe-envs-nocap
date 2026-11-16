# Issue

**Title:** Add dry-run mode and prerelease support to release workflow

## Description

## Summary

Adds `dry_run` workflow input and prerelease support to `.github/workflows/release.yml`, preconditions for the v2.1.0-beta.1 staged rollout.

## Changes (W1-W7 from the release plan)

- **W1** — Allow `workflow_dispatch` from `optimus_prime` branch when the Cargo.toml version contains `-` (prerelease only); `master` remains the source for GA. Adds `is_prerelease` and `is_dry_run` job outputs.
- **W2** — Conditional `--prerelease` flag on `gh release create` via env-level ternary (renders at YAML eval time, avoids inline bash ternary footguns). Tag creation + release creation both gated on non-dry-run.
- **W3** — Docker tag suppression for prereleases: `:latest`, `:2`, `:2.1` only apply when `is_prerelease == 'false'`. New moving `:beta` tag applies when `is_prerelease == 'true'`.
- **W5** — Header comment documenting the "never push `v*` tags manually — the workflow creates and pushes them" invariant.
- **W7** — `dry_run: boolean` workflow input. All destructive steps gated:
  - `docker-build`: `push=` in buildx outputs templatized on `is_dry_run`; digest export/upload steps skipped on dry-run.
  - `docker-merge`: download-digests + manifest-push steps skipped on dry-run; new "Dry-run manifest preview" step logs the planned tag list.
  - `smoke-test-docker`: job-level skip on dry-run (can't pull an image that was never pushed).
  - `create-tag-and-release`: per-step gates (job runs, destructive steps skip).
  - `upload-binaries`, `publish-crate`: job-level skip on dry-run.

W4 (CHANGELOG-as-release-body) is deferred to GA per the release plan. W6 (Cargo.lock mismatch guard) was already correct and is unchanged.

## Test plan

- [ ] Dispatch with `dry_run: true` from `optimus_prime` (with Cargo.toml bumped to `2.1.0-beta.1`). Expect: `check-release` outputs `is_release=true, is_prerelease=true, is_dry_run=true`; build + smoke-test-binaries pass; docker-build completes without registry push; docker-merge logs tag list via metadata-action but skips push; smoke-test-docker + upload-binaries + publish-crate all skipped; no new tag, no GH release.
- [ ] Dispatch with `dry_run: false` from `optimus_prime` publishes `2.1.0-beta.1` to crates.io; tag `v2.1.0-beta.1`; GitHub Prerelease; Docker `:v2.1.0-beta.1` + `:beta`; `:latest`/`:2`/`:2.1` untouched.
- [ ] Future GA dispatch from `master` with `dry_run: false` produces `:v2.1.0` + `:2.1` + `:2` + `:latest`; `is_prerelease=false` so the `--prerelease` flag is omitted from `gh release create`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82d1e349f5a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.