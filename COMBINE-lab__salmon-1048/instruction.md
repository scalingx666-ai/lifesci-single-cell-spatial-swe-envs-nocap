# Issue

**Title:** index: configurable sshash scratch dir (--sshashTmpDir) + memory ceiling (--ramLimit)

## Description

## Summary

A cohesive replacement for #1045. sshash's external minimizer sort wrote its
scratch to a `sshash_tmp` directory **relative to the current working
directory** and, after removing its temp *files*, left the emptied directory
behind. #1045 pruned that stray directory; this PR instead gives the caller
control over *where* the scratch lives (and how much RAM the sort may use), so
the leftover can't happen in the first place.

The two knobs already existed in `sshash-lib`'s `BuildConfiguration`
(`tmp_dirname`, `ram_limit_gib`) — they were just hard-coded at the piscem-rs
layer. This is pure plumbing across the stack:

- **piscem-rs** (published as **0.6.4**): `BuildConfig` gains `tmp_dir:
  Option<PathBuf>` and `ram_limit_gib: Option<usize>` (`None` = keep sshash's
  defaults), plus matching flags on its own `build` CLI. Salmon's dep is bumped
  `0.6.2 → 0.6.4` here.
- **salmon**: the sshash scratch now defaults to a `sshash_tmp` subdirectory of
  the build-intermediate dir — i.e. `--tmpdir` when set, else the index output
  dir — so it's co-located with the other intermediates and pruned afterwards.
  Cleanup uses **empty-only `remove_dir`**, so a caller-supplied override that is
  shared or pre-populated is never deleted, and it is retained under
  `--keepIntermediate`.

## New CLI flags (`salmon index`)

- `--sshashTmpDir <dir>` — override the sort-scratch location (e.g. a fast local
  disk), independent of `--tmpdir`.
- `--ramLimit <GiB>` — cap the external minimizer sort's memory (spills to disk
  sooner; default 8).

## Validation

- 5-case CLI matrix (default / `--tmpdir` / `--sshashTmpDir` / `--ramLimit` /
  `--keepIntermediate`): no stray `sshash_tmp` in the CWD, correct placement and
  cleanup in each; `RUST_LOG=debug` confirmed sshash receives the configured
  `tmp_dirname` and `ram_limit_gib`.
- 2 new `salmon-index` unit tests (override + keep/prune; default-build prune
  assertion added to the roundtrip test).
- Full workspace test suite green against the **published** piscem-rs 0.6.4;
  `cargo fmt` + `clippy -D warnings` clean.

Supersedes #1045.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01B7JMur5DmDpECddErpi2JS

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `54cdd903162f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.