# Issue

**Title:** fix(align): classify single-end BAM/SAM records as SingleEnd

## Description

— single-end transcriptomic BAM/SAM records dropped under stranded library types (`SF`/`SR`), reported as "0 fragments mapped".

## Root cause
In alignment mode, `frag_format`'s single-record branch (`crates/salmon-align/src/lib.rs`) classified **every** lone record as a paired-end orphan:

```rust
let status = if r.is_read1 { PairedEndLeft } else { PairedEndRight };
```

It consulted only the `0x40` first-segment flag and never `0x1` ("template has multiple segments" / paired). A genuine single-end read carries **neither** `0x40` nor `0x80`, so `is_read1` was `false` and it was mislabeled `PairedEndRight`.

`compatible_single()` for `PairedEndRight` can only satisfy paired strandedness (`SA`/`AS`), never single-end `S`/`A` — so under `SF`/`SR` every single-end alignment was discarded. `U` worked only because `es == U` short-circuits to compatible. This matches the report exactly (records with flag `0x10`, no `0x1`/`0x40`/`0x80`, e.g. from mudskipper genome→transcriptome projection).

## Fix
- Store the `0x1` (`is_segmented`) flag on `FragRecord` as `is_paired`.
- In the single-record branch, classify `!is_paired` → `MateStatus::SingleEnd`, falling back to `PairedEndLeft`/`PairedEndRight` (by `0x40`) only for a real paired-read orphan.

This mirrors salmon's `hitType` and the already-correct genome-projection (`genome_project.rs:471`) and RAD-input (`rad.rs:102`) paths. It also propagates through `--writeRad` (SingleEnd → the `SINGLE` RAD tag) so single-end BAM→RAD is tagged correctly too.

## Behavior after fix
Strand filters now respect single-end orientation instead of dropping everything. End-to-end on a synthetic single-end transcriptomic SAM (48 reverse + 12 forward records):

| libType | mapped (after fix) | before fix |
|---|---|---|
| `SR` | **48** (all reverse) | 0 |
| `SF` | **12** (all forward) | 0 |
| `U`  | **60** (all) | 60 |

Clean `quant.sf`, no "0 fragments mapped" error.

## Tests
Added regression tests:
- `single_end_record_is_single_end_and_strand_filters_apply` — a `0x1`-unset record classifies `SingleEnd`; `SF` accepts forward / `SR` accepts reverse / `U` accepts both.
- `paired_orphan_keeps_left_right_status` — a `0x1`-set lone record stays `PairedEndLeft`/`PairedEndRight` (unchanged).

`cargo fmt --all --check`, `clippy -p salmon-align`, and the salmon-align/salmon-core suites are clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01B7JMur5DmDpECddErpi2JS

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6914c29958d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.