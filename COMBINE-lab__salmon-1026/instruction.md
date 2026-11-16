# Issue

**Title:** fix(quant): count num_mapped after the strand-compatibility filter (stranded over-count, #1025)

## Description

## What

Count a fragment as mapped only after it passes the strand-compatibility filter, matching C++ salmon. .

## Why

In reads (SA/sketch) mode, `record()` incremented `num_mapped` for every fragment with any mapping, **before** the strand-compatibility filter. On a stranded library, a fragment whose every mapping is strand-incompatible is then dropped (`compat.is_empty() -> return`) and contributes no mass, but it had already been counted as mapped. This inflated `num_mapped` / `percent_mapped` / `num_compatible_fragments` / `num_assigned_fragments` and broke the invariant `Σ NumReads == num_mapped`. Unstranded libraries are unaffected (the filter never empties `compat`), and C++ salmon counts mapped post-filter, so it keeps the invariant.

Same reads (GRCh38 r115 decoy gentrome, one real PE sample, no bias flags):

| run | detected lib | `num_mapped` | `Σ NumReads` | gap |
| --- | --- | --- | --- | --- |
| C++ salmon 1.12.0 `-l A` | ISF | 275565 | 275565 | 0.00% |
| 2.1.0 `-l A` (before) | ISF | 311967 | 295597 | 5.25% |
| 2.1.0 `-l IU` | IU | 311967 | 311967 | 0.00% |

## Change

`crates/salmon-quant/src/processor.rs`:
- Move the `num_mapped` increment (and the orphan classification) to **after** the `compat.is_empty()` check.
- Library-type auto-detection still samples observed formats from the raw mappings, before the filter (unchanged behavior).
- Orphan classification now keys off the best **compatible** mapping (identical for unstranded libraries, where the filter keeps every mapping).

Alignment-based (`-a`) mode uses a separate counter and is untouched.

## Testing

- New regression test `stranded_num_mapped_matches_quantified_mass` (`crates/salmon-quant/tests/quant_end_to_end.rs`): asserts `Σ NumReads == num_mapped` and that strand-incompatible fragments (inward FR reads quantified under the opposite stranded type `ISR`) are not counted as mapped. Fails before this change (`num_mapped = 1000 / 1000`), passes after.
- `cargo test --workspace`: 152 passing.
- `cargo fmt --all --check`: clean.
- `cargo clippy` on the changed crate: no findings in the changed files. (Two pre-existing `clippy` 1.95.0 lints in `salmon-model`/`salmon-map`, unrelated to this change, are left untouched.)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8aa59a56d660`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.