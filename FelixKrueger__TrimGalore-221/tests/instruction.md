# Issue

**Title:** docs(cli): flag-by-flag help-text polish

## Description

## Summary

Flag-by-flag audit of the Rust `--help` output against the Perl v0.6.11 help text. Twenty-five docstring edits in `src/cli.rs` plus one callout in the user guide. No behavioural changes — the binary runs identically.

## Accuracy fixes (three actively-wrong claims caught)

- **`--paired`**: removed stale "Expects exactly 2 input files" — beta.2 accepts an even number of input files as N R1/R2 pairs
- **`--illumina`**: "This is the default" → "Also the auto-detect fallback" (more precise; wasn't strictly "default" when a preset is active)
- **`--keep`** (hidden): "Not yet supported" → architectural no-op clarification (permanent, not pending)
- **`--rename` format**: now reflects that `:clip5:` / `:clip3:` each appear only when that side was clipped
- **`--hardtrim5/3` filenames**: suffix now matches actual Rust format (`.<N>bp_5prime.fq(.gz)`), with the `bp` insertion that Perl doesn't use

## Detail / cross-ref additions

- Preset side-effects surfaced: `--small_rna` (`--length → 18` + `--adapter2` default), `--rrbs` directional auto-set `--clip_R2 2`
- Auto-detect coverage gaps flagged on `--stranded_illumina`, `--bgiseq`
- Paired-end semantics added to `--length`, `--max_n`, `--retain_unpaired`
- **`--rrbs` Tecan Ovation kit incompatibility warning** (foot-gun documented in Perl, dropped in Rust)
- Multi-adapter syntax (`file:` / repeat) noted on `--adapter` / `--adapter2`
- Use-case hints on `--clip_R1/R2`, `--three_prime_clip_R1/R2` (incl. bisulfite M-bias), `--max_length` (smallRNA-only)
- `--cores` scaling language tightened ("up to ~16" → "through at least 16"; matches benchmark data in `Docs/SUMMARY.md`)
- `--suppress_warn` / `--keep` deprecated-flag messages rephrased in user-facing terms

## User guide

One `> [!NOTE]` callout at the top of Step 1 in `Docs/Trim_Galore_User_Guide.md` flagging the single-pass architecture (vs. the Perl-inherited staged-subprocess framing). A full user-guide refresh is tracked as a follow-up — the guide still describes Trim Galore as a Cutadapt wrapper in several places.

## Follow-ups surfaced by the walk

Eight behavioural/migration questions logged for separate triage (not addressed in this PR):

1. User guide v2 rewrite (Perl-era framing throughout)
2. Additional adapter-spec detail for the user guide
3. `A{N}` brace expansion — supported in Perl, not in Rust
4. BGISEQ / STRANDED_ILLUMINA auto-detection probe set
5. `-r1` / `-r2` single-dash migration foot-gun (clap parses as `-r=1`)
6. `--trim-n` + `--rrbs` byte-identity exception (Perl silently skipped; Rust trims)
7. `--hardtrim` filename rename (`.Nbp_*prime` vs Perl's `.N_*prime`)
8. `--poly_a` direction auto-detect (Perl detects A vs T; Rust hardcodes)

## Verification

- [x] `cargo build --release` — clean
- [x] `cargo test --release` — 106 passed
- [x] `cargo clippy --all-targets --release -- -D warnings` — silent
- [x] `cargo fmt --all -- --check` — silent
- [x] `./target/release/trim_galore --help` — renders cleanly, 168 lines (same length, denser per line)

## Test plan

- [ ] Scan the rendered `--help` diff
- [ ] Spot-check the `--paired` fix (must no longer say "exactly 2")
- [ ] Verify the `--hardtrim5/3` filename claim matches real output

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2fcaab17a038`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.