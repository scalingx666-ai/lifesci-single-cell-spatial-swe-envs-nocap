# Issue

**Title:** polish(multi-pair): name both colliding paths, catch duplicate-pair typo, add Cli::validate tests

## Description

## Summary

Five improvements surfaced by a dual independent review of the multi-pair regression fix (commits `1b57ebd` / `8a6cfc5` / `aa92493` on `optimus_prime`). UX polish + test coverage on top of already-shipped behaviour — no new features, no new flags.

- **`src/main.rs`** — collision pre-flight now keeps `HashMap<String, PathBuf>` keyed on ASCII-lowercase and names *both* the previously-claimed and newly-claimed paths in the error. The previous `HashSet<String>` only knew one.
- **`src/cli.rs`** — dedicated `Pair N ({r1}, {r2}) is a duplicate of pair M` error for accidental copy-paste of the same pair twice. Previously tripped the APFS/NTFS collision check with a misdirecting message; now caught early in `Cli::validate()` with a precise message, leaving the collision check to catch its actual purpose (different inputs → same outputs via case folding).
- **`src/cli.rs`** — `#[cfg(test)] mod tests` with 7 tests covering odd-count / within-pair-equal / cross-pair-duplicate / multi-pair-basename rejections plus three regression guards (SE `--basename`, 2-file paired golden, `--clock` strict-2).
- **`CHANGELOG.md`** — two addenda inside the existing collision-fix bullet: opt-in case-sensitive APFS/ZFS caveat, and partial-failure no-rollback note (matches v0.6.x Perl behaviour).

## Test plan

- [x] `cargo build --release` — clean
- [x] `cargo test --release` — 106 tests pass (99 existing + 7 new)
- [x] `cargo clippy --all-targets --release -- -D warnings` — silent
- [x] `cargo fmt --all -- --check` — silent
- [x] Manual UX: `A_R1 A_R2 A_R1 A_R2` → `Pair 2 (...) is a duplicate of pair 1`
- [x] Manual UX: case-differing pairs in separate dirs → `Output path collision (case-insensitive, for APFS/NTFS safety): /.../sample_R1_val_1.fq.gz and /.../SAMPLE_R1_val_1.fq.gz ...` (both paths named, output dir stays empty)
- [ ] CI green on all 5 gates (lint, reproducibility, tests, audit, Perl validation)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6cae5c344b32`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.