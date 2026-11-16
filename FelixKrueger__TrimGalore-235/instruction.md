# Issue

**Title:** fix(report): MultiQC-parity gaps surfaced in nf-core pre-GA review

## Description

## Summary

The nf-core/rnaseq team filed a [pre-GA validation report](#) on v2.1.0-beta.5 yesterday — three issues filed (#232, #233, #234) plus four acknowledged-as-design report-text changes. **Trimmed FASTQ records remain byte-identical to Perl v0.6.10** across the smoke matrix; every filed issue is in the trimming-report *text*, not the data layer.

This PR  + #233 in code and covers #234 plus the four acknowledged changes via a CHANGELOG migration note.

## What changed

### #232 — RRBS samples: cutadapt-section "Total written (filtered)" drifts from v0.6.x

Beta.4's `eedbc66` ("Fix cutadapt-section report to match v0.6.x MultiQC-parsed values") introduced `total_bp_after_trim` for MultiQC parity, but incremented it *after* the full per-read pipeline — including the `--rrbs` 2 bp 3' truncation. The reported value drifted from v0.6.x by `RRBS-trimmed-reads × 2 bp`.

Fix: capture `bp_after_cutadapt: usize` on `TrimResult` immediately after quality + adapter trim and **before** RRBS / poly-A/G / N-trim / clipping. Use that for `total_bp_after_trim` in both single-end (`src/trimmer.rs:run_single_end`) and paired-end (`src/trimmer.rs:run_paired_end`) pipelines.

### #233 — RUN STATISTICS filter-removed lines omitted at zero count

`src/report.rs` had four `if stats.X > 0` guards (`too_short`, `too_long`, `too_many_n`, plus PE counterpart `pairs_removed_n`). v0.6.x always emits these even when zero. MultiQC's canonical fallback parser greps for the literal line as the "100% passing" path — guarding broke that parser on samples that pass everything.

Fix: drop the guards. The existing `percentage()` helper already returns `0.0` on zero denominator, so zero-count rendering is safe.

### #234 — RRBS quality-trim line shape (CHANGELOG only)

v0.6.x emits `Sequences were truncated to a varying degree because of deteriorating qualities …: N (P%)` on RRBS (counts *reads*); v2.x emits the cutadapt-style `Quality-trimmed: N bp (P%)` (counts *bp*). Reviewer flagged this as "arguably wontfix" because v2.x is more consistent across modes. Documented in the v2.1.0 migration notes alongside the four acknowledged design changes (dropped adapter family-name annotation, omitted "Bases preceding removed adapters" histogram, dropped per-adapter "Minimum overlap" line, modern Cutadapt `floor(L × error_rate)` `max.err` formula).

## Test plan

- [x] `cargo build --release` — clean
- [x] `cargo test --release` — **165 passed** (was 161; +2 for #232 RRBS pre-truncation capture, +2 for #233 zero-count emission on SE and PE paths)
- [x] `cargo fmt --all -- --check` — clean after auto-format
- [x] `cargo clippy --all-targets --release -- -D warnings` — clean
- [x] Manual review against the nf-core report's cited line numbers (`src/trimmer.rs:148-175,326`, `src/report.rs:597,606,614,407`) — all match
- [ ] CI green

## Validation against the report's claims

| Reviewer claim | Verified against current `optimus_prime` HEAD |
|---|---|
| `total_bp_after_trim` at `trimmer.rs:326` after RRBS truncation | ✅ confirmed |
| `if stats.too_short > 0` guard at `report.rs:597` | ✅ confirmed |
| Same pattern at `too_long` (line 606) and `too_many_n` (line 614) | ✅ confirmed |
| PE pair-removal counterpart guard | ✅ found at `report.rs:407` (`pairs_removed_n`) |

## Closes

-
-
- Documents #234 (left open until reviewer agrees the CHANGELOG note is sufficient)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `488d82fdd168`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.