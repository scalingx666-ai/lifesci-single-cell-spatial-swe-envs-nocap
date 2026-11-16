# Issue

**Title:** fix(report): cap adapter-table expect and max.err at the adapter length

## Description

## Problem

The "Overview of removed sequences" table in the text report computes, for each removed length `L`:

- `expect = n / 4^L`
- `max.err = floor(error_rate * L)`

Cutadapt caps `L` at the adapter's length in both (`min(length, effective_length)` in its histogram code), because a removal longer than the adapter cannot match more adapter bases. Each adapter section uses its own adapter length, so multi-adapter runs are capped per adapter.

On `test_files/nextera_100K.fastq.gz` with `--nextera` (12 bp adapter), compared with the bundled Cutadapt 1.18 report `test_files/nextera_100K.fastq.gz_trimming_report.txt`:

| length | Cutadapt 1.18 max.err | ours before |
|---|---|---|
| 20-29 | 1 | 2 |
| 30-39 | 1 | 3 |
| 40-49 | 1 | 4 |
| 50-51 | 1 | 5 |

`expect` has the same issue: it kept falling towards 0 past the adapter length instead of levelling off at `n / 4^12`. On 100K reads both round to 0.0, but on large inputs (for example 100 M reads: 6.0 at length 12) the uncapped value goes wrong in MultiQC's obs/exp plot.

## Fix

`let capped = length.min(seq.len());` used in both formulas in `write_cutadapt_compatible_section`. The JSON report does not carry these columns, so it is unchanged.

## Testing

- New unit test `report::tests::test_adapter_table_caps_expect_and_max_err_at_adapter_length`: 13 bp adapter, `n = 4^13`, one removal each at lengths 13 and 20. Hand-derived expected rows: `13 1 1.0 1 1` and `20 1 1.0 1 1`. Without the fix the test fails (length 20 printed `20 1 0.0 2 1`).
- Regenerated reports for `nextera_100K.fastq.gz` (`--nextera`) and `smallRNA_100K.fastq.gz` (`--small_rna`): the length, expect and max.err columns are now identical to the bundled Cutadapt 1.18 reports (`diff` empty; before the fix nextera differed on 29 rows).
- `cargo test`: 846 passed, 0 failed. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No FASTQ output changes, so the Perl 0.6.11 validation matrix (which md5-compares trimmed FASTQ) is unaffected. The text report changes on purpose: rows whose length is greater than the adapter length now show the capped `expect` and `max.err`, matching what Cutadapt (and so Perl Trim Galore) wrote.

## Suggested CHANGELOG entry

- **The adapter table's `expect` and `max.err` columns now match Cutadapt.** For removed lengths longer than the adapter, both are now computed at the adapter length, as Cutadapt does. With the 12 bp Nextera adapter, length 20 showed `max.err` 2 where Cutadapt shows 1, and `expect` (used by MultiQC's obs/exp plot) dropped towards 0 instead of levelling off.

Part of #546 (finding 8 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c98c98b56b96`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.