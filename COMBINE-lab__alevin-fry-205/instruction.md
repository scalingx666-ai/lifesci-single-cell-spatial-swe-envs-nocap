# Issue

**Title:** fix(utils): parse pre-release and build version strings without panicking

## Description

## Summary

`InternalVersionInfo::from_str` called `unwrap()` on the `u32` parse of every dot-separated part of the version string. Any part that wasn't a number panicked instead of returning the `VersionParseError` the function already declares. `collate`, `atac sort` and `atac collate` use this function to parse two strings: their own version (`CARGO_PKG_VERSION`) and the `version_str` stored in `generate_permit_list.json`. That has two consequences:

- A pre-release build such as `0.19.0-rc.1` panics on the permit list it just wrote. Every collate fails, so pre-release test builds can't be tagged.
- Any release panics on a permit list written by a pre-release or hand-edited build. For example, `0.18.3-dev` gives `ParseIntError { kind: InvalidDigit }` at `src/utils.rs:1266:73`.

The bug can't trigger today, because alevin-fry's own version has never been a pre-release. It would fire on the first `-rc` bump in the RAD v2 release train.

## Changes

- `InternalVersionInfo::from_str` is now lenient and returns errors instead of panicking:
  - It strips one leading `v`, which is the form `Display` prints.
  - It drops a `-pre-release` and/or `+build` suffix.
  - It requires exactly three `u32` parts.
  - Anything else returns `VersionParseError::IncorrectFormat`, carrying the original string. The error type and its message are unchanged.
- Pre-release versions compare as their core version, and this is documented on the struct:
  - `is_compatible_with` still compares only major.minor.
  - The newly derived `PartialOrd`/`Ord` on (major, minor, patch) treats `0.19.0-rc.1` as equal to `0.19.0`, rather than placing it before `0.19.0` as semver does.
- The stale `#[allow(dead_code)]` is removed. `Display` and `is_compatible_with` read the fields, and clippy reports no new warnings.
- New unit tests cover:
  - accepted: `0.19.0-rc.1`, `0.18.3-dev`, `0.15.0+build.5`, `1.2.3-beta.2+abc`, `v1.2.3`
  - rejected without a panic, with the original string in the error: `""`, `1.2`, `1.2.3.4`, `a.b.c`, `1..3`, `1.2.x`, `vv1.2.3`, `-1.2.3`, `"1.2.3 "`
  - pre-release compatibility and ordering, and a `Display` round trip

## Behavior/compatibility

- Every plain `x.y.z` parses exactly as before.
- Strings that were already errors are still errors, with the same message. This covers wrong part counts such as `0.18` and `1.2.3.4`.
- Inputs that used to panic now either parse to their core version (`0.18.3-dev`, `v0.18.3`, `0.18.3+abc`) or return the clean `IncorrectFormat` error (`a.b.c`, `""`).
- One other change: Rust's `u32::from_str` accepts a part with an explicit plus sign, so the old code accepted `+0.18.3` and `0.+18.3`. Now the `+` starts build metadata and those strings are rejected. No alevin-fry release writes such a string, because Cargo versions are semver. An exhaustive comparison of the old and new parsers over every string of length 7 or less, drawn from the characters `0 1 9 . v - + a` and space, found only this divergence. All 891 cases are plus-signed parts that went from Ok to Err.
- The major.minor gate is unchanged. A `0.19.0-rc.1` build accepts any `0.19.x` permit list and rejects a `0.18.3` one with the usual "please regenerate" error.
- Pipeline outputs are unchanged: this changes only how version strings are parsed.
- A `collate` error still exits through `main.rs`'s `.expect("could not collate.")` with exit code 134. That code is out of scope here. The difference is that the message is now the real version error instead of a `ParseIntError` unwrap.

## Testing

- `cargo fmt --check`: clean.
- `cargo clippy --all-targets`: 0 warnings on both base and branch.
- `cargo test`:
  - base: 108 passed, 3 ignored
  - branch: 111 passed, 3 ignored (the 3 new tests)
  - The 3 new tests panic at `utils.rs:1266:73` when run against develop's parser.
- Runtime, comparing `collate` from develop with this branch on a real permit list whose `version_str` was edited:
  - `0.18.3-dev`, `0.18.0-rc.1`, `0.18.3+abc`, `v0.18.3`: develop panics with `ParseIntError`; the branch succeeds.
  - `a.b.c`, `""`, `0.17.0-rc.1`: develop panics with `ParseIntError`; the branch gives the format error, or the major.minor incompatibility error for `0.17.0-rc.1`.
  - `0.18.3`, `0.18`, `1.2.3.4`, `0.17.0`: same result on both.
  - `atac sort` with `0.18.3-dev`: develop panics; the branch writes a `map.bed` byte-identical to the run with `0.18.3`.
- Same pipelines, same outputs. These runs used `generate-permit-list`, `collate` and `quant -r cr-like` with `-t 1`, which the thread floor raises to 2. The develop binary and this branch's binary were run from the same path into the same output directory, and outputs were compared by name, not by row order. Byte-level comparison doesn't work across builds: develop gives different bytes than this branch, and on PBMC two develop runs differ from each other.
  - Tiny scRNA (RAD v2): JSON metadata, the collated RAD (16,148 records grouped by CB), the matrix ((barcode, gene) → count, 2,200 nonzeros), `featureDump` and the `quant.json` cell lists mapped to barcodes are all identical.
  - PBMC 10x v3 (162 MB RAD, `--knee-distance`): the same checks are identical, with 1,162 cells, 3,566,459 collated records and 926,835 nonzeros.
  - scATAC (`atac generate-permit-list` and `atac sort`): `map.bed` is byte-identical (813,909 lines).
- Cargo version bumped to `0.19.0-rc.1` in scratch copies:
  - develop builds pass their tests, because those tests use a fixed `"0.12.0"`. Its `collate` panics on its own permit list.
  - This branch's build runs gpl, collate and quant to completion, and its tests pass (111).
  - `test/rad-v2-integration` (develop + #202 + #203 + #204) with the rc bump: 10 tests fail with the `utils.rs` panic.
  - The same branch merged with this PR and rc-bumped: 130 passed, 0 failed.

## Merge notes

- **Suggested order** for this release: #203 (`fix/flex-sample-names`), #202 (`feat/200-umi-read-counts`), this PR, `chore/rad-v2-release-hygiene`, `fix/errors-instead-of-panics`, and last #204 (`feat/probe-sum`) updated with `fix/204-explicit-flex-data-type`.
- **Heads checked on 2026-10-22:** develop edfd1aa, #202 8011bd5, #203 64c24d9, #204 d01f955, this branch 33154af. None of them has moved since the previous check.
- **Clean merges.** This PR changes only `InternalVersionInfo` in `src/utils.rs`. It merges cleanly onto develop. It also merges cleanly with #202, #203, #204, each sibling branch and `test/rad-v2-integration`.
- **Merged trees**, run without the rc bump:

| Merged tree | `cargo test` | clippy |
|---|---|---|
| #203 + this PR | 114 passed (#203 alone: 111) | 0 warnings |
| #202 + this PR | 119 passed | 0 warnings |
| #204 + this PR | 116 passed | 0 warnings |
| `test/rad-v2-integration` + this PR | 130 passed (branch alone: 127) | 0 warnings |
| The whole merge, in the order above | 142 passed, 0 failed, 3 ignored | 0 warnings (also with `--all-features`); fmt clean |

- **#203's version check.** #203 adds its own lenient `parse_release_version` and a `FIRST_ORDINAL_SAMPLE_COLLATE` tuple in `quant.rs`. Only `ensure_ordinal_sample_indices` uses them. This PR leaves #203's code alone.
  - Once both PRs merge, that check could instead use `InternalVersionInfo::from_str(version).ok()`. It would compare against `InternalVersionInfo { major: 0, minor: 15, patch: 0 }` with the new `Ord`, and keep "unparseable ⇒ accept".
  - That change has one difference to accept. `parse_release_version` takes the first three runs of digits, so it also accepts strings like `1.2.3.4` or `alevin-fry 0.15.0`. This parser rejects them, so under "unparseable ⇒ accept" they would be accepted. In practice this doesn't matter, because alevin-fry only writes `CARGO_PKG_VERSION`.
  - #203 switches to `TEST_VERSION = env!("CARGO_PKG_VERSION")`, and that switch is what makes the test suite fail on a pre-release bump. This PR fixes that without touching #203's code.
- **Not in this PR:**
  - 1b3de59 on `test/rad-v2-integration` makes `--dump-molecules` work on Flex probe-level data. It belongs with whichever of #202 and #204 merges second (#204 in this order).
  - simpleaf's `feat/multiplex-quant-new-alevin-fry-options` passes `generate-permit-list --data-type flex`. It must ship with or after the alevin-fry release that contains #204 and `fix/204-explicit-flex-data-type`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01TtmwfkBMvwsCxdQrf4RTPN

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edfd1aae5426`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.