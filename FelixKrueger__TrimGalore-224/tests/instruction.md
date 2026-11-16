# Issue

**Title:** fix(specialty): multi-pair --clock and --implicon (same shape as beta.2 --paired fix)

## Description

## Summary

Same regression as the `--paired` beta.1 → beta.2 fix, on a different code path. `--clock` and `--implicon` validation rejected anything other than exactly 2 input files, and `main.rs` dispatch hardcoded `cli.input[0]` / `cli.input[1]` indexing. Users running shell-glob invocations like `trim_galore --implicon --paired *fastq.gz` (the exact pattern reported by Felix) hit:

```
Error: --implicon requires exactly 2 paired-end input files
```

This PR widens both specialty modes to accept multi-pair input, with the same safety net as `--paired`: even-count + within-pair byte-equal R1≠R2 + cross-pair duplicate-pair detection + output-collision pre-flight.

## Changes

### Refactor: shared `validate_paired_input` helper

Extracted `Cli::validate_paired_input(mode_label)` in `src/cli.rs` from the inlined `if self.paired { … }` block. Now reused for `--paired`, `--clock`, and `--implicon` — single source of truth for pairwise-input validation. Error messages name the calling mode explicitly (e.g., `"--clock mode requires an even number of input files (R1/R2 pairs), got 3"`).

### Refactor: shared `run_specialty_paired` dispatch helper

`src/main.rs` gains `run_specialty_paired(cli, mode_label, output_names_fn, run_pair_fn)`. Loops `cli.input.chunks(2)`, prints a per-pair header (`=== Clock pair N of M ===` / `=== IMPLICON pair N of M ===`) for multi-pair invocations, and runs an output-collision pre-flight (case-insensitive for APFS/NTFS safety) before any I/O. Per-pair errors are wrapped via `.with_context` so a failing pair K identifies itself in the error message.

### Visibility tweak

`clock_output_name` / `implicon_output_name` in `src/specialty.rs` widened from private to `pub` so the dispatch helper can use them in the collision pre-flight. They were already computing the canonical output names; now they're reused rather than duplicated inline.

### Tests

Replaced the now-obsolete `test_validate_clock_still_requires_exactly_2` (regression guard for the strict-2 assumption) with **7 new tests**:

- `test_validate_clock_two_pairs_accepted`
- `test_validate_clock_odd_count_rejected`
- `test_validate_clock_r1_equal_r2_within_pair_rejected`
- `test_validate_clock_duplicate_pair_rejected`
- `test_validate_implicon_two_pairs_accepted`
- `test_validate_implicon_odd_count_rejected`
- `test_validate_implicon_duplicate_pair_rejected`

### Documentation

Added a `> [!NOTE]` block at the top of Step 4 (Specialised Trimming) in `docs/Trim_Galore_User_Guide.md` covering multi-pair behaviour across all three specialty modes (`--hardtrim5`, `--hardtrim3`, `--clock`, `--implicon`) with the same pairwise-order caveat that applies to `--paired`.

## Codebase audit (post-commit)

Confirmed no other lurking `cli.input[0]` / `cli.input[1]` single-pair assumptions:

```
$ grep -nE 'cli\.input\[[01]\]|self\.input\[[01]\]' src/*.rs
src/main.rs:37:    FastqReader::sanity_check(&cli.input[0])?;
```

The remaining match at `main.rs:37` is a benign sanity-check (early-fail on a missing/malformed first file) that doesn't make a multi-pair assumption — the dispatch code afterwards handles however many files were passed. **Net single-pair-assumption sites in the codebase: zero.**

## Verification

- [x] `cargo build --release` — clean
- [x] `cargo test --release` — **153 passed** (147 + 6 new)
- [x] `cargo clippy --all-targets --release -- -D warnings` — silent
- [x] `cargo fmt --all -- --check` — silent
- [x] Live smoke: `--clock` with 4 inputs (2 pairs) → 4 outputs with correct `.clock_UMI.{R1,R2}.fq.gz` filenames
- [x] Live smoke: `--implicon` with 4 inputs (2 pairs) → 4 outputs with correct `_8bp_UMI_{R1,R2}.fastq.gz` filenames
- [x] Negative test: cross-source-dir pair pairs that produce identical output filenames are caught by the collision pre-flight before any I/O

## Test plan

- [ ] `gh pr checks N` — confirm 5/5 gates green
- [ ] Spot-check the per-pair `=== Clock pair N of M ===` / `=== IMPLICON pair N of M ===` headers on a multi-pair invocation
- [ ] Confirm the existing single-pair smoke (CI step) for `--clock` / `--implicon` (if any) still passes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `246af7125580`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.