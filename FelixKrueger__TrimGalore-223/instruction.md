# Issue

**Title:** User-guide v2 refresh + 2 bugs surfaced during review

## Description

## Summary

Rewrites the user guide (`docs/Trim_Galore_User_Guide.md`) to match v2.x reality, dropping Perl-era framing, phantom-flag documentation, and a ~220-line duplicate of `--help` that had been silently drifting out of sync on every recent `--help` edit. Also fixes two real bugs that shook out during the refresh.

## User-guide sections (A → D)

- **Section A (`1ccc896`)** — Intro + Steps 1–4 framing. Drops "wrapper script that uses Cutadapt" as current-tense; reframes as historical context. Updates Step 2 language from "Cutadapt finds and removes adapter sequences" to "Trim Galore finds and removes". Adds BGI/DNBSEQ to the auto-detect probe list; adds the Stranded-Illumina-not-probed note. Updates multi-adapter example to lead with the cleaner repeatable form.

- **Section B (`ba8d9f5`)** — Replaces the ~220-line "Full list of options" duplicate with a ~30-line "Flag reference" section focused on cross-flag interactions. Phantom-flag documentation for `-t/--trim1` (doesn't exist in Rust *or* Perl v0.6.11 — just guide drift) and the obsolete `--keep` discussion are removed. Kept and preserved: Tecan Ovation kit caveat and MseI-digested libraries note. **Biggest maintenance win**: future `--help` docstring edits no longer risk drifting out of sync with a duplicate in the guide.

- **Section C (`ad6c309`)** — Light touch on specialty-modes section. Adds missing IMPLICON subsection (was completely omitted from the original guide despite being a first-class run-and-exit mode). Fixes "In it's" typo. Clarifies the clock post-processing command — `*R1.fq.gz *R2.fq.gz` globs expand to all-R1s-then-all-R2s, which fails `--paired` pairwise validation in multi-sample cases.

- **Section D (`e87e146`)** — Aligns the "Understanding the trimming reports" section with actual v2.x output. Generated a real report and diffed line-by-line against the guide's claims. Dropped Perl-era entries v2.x does not emit: `Cutadapt version:`, `Python version:`, per-core annotation, clip-status lines, FastQC line, `Finished in X.XX s (...)` line, `Bases preceding removed adapters:` block. Updated the Cutadapt-compat example banner (`This is cutadapt 3.4 with Python 3.9.6` → `Trim Galore 2.1.0 (Oxidized Edition) — adapter trimming built in` + `This is cutadapt 4.0 (compatible; for MultiQC backwards compatibility)`).

## Bugs shook out during review

- **`fix(adapter)` (`92c77af`)** — implemented repeatable `-a` / `-a2`. The help-text docstrings added in PR #221 and the README rhetoric from PR #222 had been claiming this worked for three commits, but it errored with `the argument '--adapter <ADAPTER>' cannot be used multiple times` because the field was `Option<String>`. Fixed by changing to `Vec<String>` with a renumber loop in `main.rs::resolve_adapter`. Also extended `rewrite_perl_short_flags` to cover `-a2` (same foot-gun category as `-r1`/`-r2`: clap would parse `-a2 SEQ` as `-a=2` with `SEQ` as stray positional). 4 new unit tests.

- **`fix(report)` (`cdcc901`)** — dropped the stray `-end` suffix from the paired-end length-cutoff line in the text trimming report (known cosmetic bug flagged in project memory pre-beta.1). Was producing `Minimum required sequence length for both reads before a sequence pair gets removed-end: 20 bp`. Now emits cleanly: `...gets removed: 20 bp`. Single-end branch unchanged.

## Stats

- User guide: **534 → 325 lines** (−209 net; the big delete was Section B)
- Tests: **144 passing** (141 pre-branch + 3 from the `-a2` rewrite + 1 end-to-end parse-from test)
- clippy + fmt: clean

## Verification

- [x] `cargo build --release` — clean
- [x] `cargo test --release` — 144 passed
- [x] `cargo clippy --all-targets --release -- -D warnings` — silent
- [x] `cargo fmt --all -- --check` — silent
- [x] Generated real v2.x reports (single-end + paired-end with clipping options) and diffed against the user guide — Section D now matches line-for-line
- [x] Live smoke: `-a AGCT -a TTTA -a2 GCAT -a2 AAAA` produces both R1 and R2 adapter lists with 2 entries each
- [x] Paired-end report now emits correct "...gets removed: 20 bp" (no stray `-end`)

## Test plan

- [x] Scan the `docs/Trim_Galore_User_Guide.md` diff — biggest block is the Section B delete, should be straightforward
- [ ] Confirm `Validate vs Perl TrimGalore` CI stays green (the `--a2` rewrite and the `-a`/`Vec<String>` change touch the argv-parsing pipeline but existing Perl-compat fixtures use single `-a` invocations)
- [ ] Spot-check one real trimming report to confirm the `-end` suffix is gone

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0af1e98c9bd2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.