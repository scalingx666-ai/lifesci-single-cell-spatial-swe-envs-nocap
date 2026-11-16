# Issue

**Title:** Pre-GA polish: A{N} shorthand, BGI auto-detect, Perl-parity fixes, rhetoric reframe

## Description

## Summary

Bundle of pre-GA polish work aimed at closing out Perl-migration gaps and repositioning the rewrite's voice now that v2.x has genuine capability beyond v0.6.x. Eight commits, all small and cohesive.

## What's in

### New capabilities (beyond Perl v0.6.x)

- **`A{N}` brace shorthand for `--adapter` / `--adapter2`** (`181bfa6`). `-a A{10}` now expands to `-a AAAAAAAAAA`, matching Perl v0.6.x semantics verbatim. Hand-written matcher — no new crate dependencies. Only applies to single-adapter specs, not multi-adapter or FASTA entries (matches Perl).
- **BGI/DNBSEQ added to auto-detection probe set** (`0a14dbc`). Users running BGI/MGI/DNBSEQ data no longer need `--bgiseq` explicitly; the 32bp probe runs alongside Illumina/Nextera/smallRNA. Stranded Illumina stays explicit-only (its sequence is too similar to Nextera to probe reliably). Tie-break preserved — zero-count still defaults to Illumina.

### Perl-parity fixes (restore v0.6.x behaviour)

- **`--trim-n` suppressed under `--rrbs`** (`4aaa4af`). Perl's RRBS Cutadapt invocations at `trim_galore:862–1330` omit `$trim_n`; Rust applied it unconditionally. Three-line gate in `src/trimmer.rs:220–223` restores parity.
- **Perl-era `-r1` / `-r2` short flags parse correctly** (`9b2d873`). Clap single-char rule meant `-r1 40` silently parsed as `-r=1` with `40` as a stray positional → confusing "odd count" error. Added a small pre-parse rewrite (`cli::rewrite_perl_short_flags`) that rewrites the exact tokens to `--r1` / `--r2` (the existing long aliases) before clap sees them.

### Test coverage

- **Unit tests for `--clock` and `--implicon`** (`a5889f2`). These specialty modes had zero direct test coverage — only one CLI-parse assertion. Added 6 tests covering UMI extraction, read-ID rewriting, sequence clipping, and too-short-input error paths.

### Docs / positioning

- **"Byte-identical" → "faithful rewrite"** (`ccd198c`). v2.x has genuine additions beyond Perl (`--poly_g`, generic `--poly_a`, per-pair adapter detection, build provenance, etc.) — the old rhetoric no longer fits. Updated in README, User Guide, SUMMARY, CHANGELOG, and `src/cli.rs` help preamble. The two benchmark-section "byte-identical" mentions stay (they mean "deterministic across `--cores`", still true).
- **README feature-list updates** (`d403bfd`, `c393d9d`): BGI auto-detection now listed alongside Illumina/Nextera/smallRNA; multi-adapter example updated from Perl's embedded-string `-a " SEQ1 -a SEQ2"` hack to the cleaner repeatable `-a`/`-a2`.

## Follow-up audit of the original 8-item list

| # | Item | Outcome |
|---|---|---|
| 1 | User guide v2 rewrite | Deferred to separate `docs/user-guide-v2-refresh` branch |
| 2 | Additional adapter-spec detail | Folds into #1 |
| 3 | `A{N}` brace expansion | ✅ Implemented (`181bfa6`) |
| 4 | BGI/STRANDED_ILLUMINA auto-detect | ✅ BGI added; stranded deliberately out (`0a14dbc`) |
| 5 | `-r1` / `-r2` migration foot-gun | ✅ Fixed (`9b2d873`) |
| 6 | `--trim-n` + `--rrbs` byte-identity | ✅ Fixed (`4aaa4af`) |
| 7 | `--hardtrim` filename rename | Cleared — phantom issue (Perl help text was wrong, Perl source actually matches Rust) |
| 8 | `--poly_a` direction auto-detect | Cleared — Perl's `--polyA` was a Thermo Fisher kit-specific feature, removed entirely; Rust's `--poly_a` is intentionally generic |

## Verification

- [x] `cargo build --release` — clean
- [x] `cargo test --release` — **140 passed** (was 106 before this branch; +34 net)
- [x] `cargo clippy --all-targets --release -- -D warnings` — silent
- [x] `cargo fmt --all -- --check` — silent
- [x] Live smoke: `-a "A{8}"` → `Adapter sequence A{8} expanded to AAAAAAAA`
- [x] Live smoke: BGI fixture → `Using BGI/DNBSEQ adapter for trimming (count: 200)`
- [x] Live smoke: `-r1 40 -r2 35` → pipeline runs cleanly (previously errored on "odd count")

## Test plan

- [x] Scan the `--help` diff vs. base (the docstring edits on `--bgiseq`, `--trim-n`, `--adapter`, `--adapter2`, and the top-level `about` preamble)
- [ ] Spot-check the rhetoric change reads sensibly in all five files
- [x] Confirm CI `Validate vs Perl TrimGalore` stays green (it already passed on the same byte-identical CI steps at `hardtrim5`; nothing in the new code path interacts with those fixtures)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `76ea70730f10`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.