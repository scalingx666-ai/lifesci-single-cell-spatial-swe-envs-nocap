# Issue

**Title:** fix(clock): label the CAGT count as the pairs that lack it

## Description

## Problem

The `--clock` summary (`src/specialty.rs`) counts read pairs whose fixed sequence (bases 9-12) is not `CAGT` in R1 or R2, but prints that number under the opposite label:

```
Sequences processed in total: 10000
thereof had fixed sequence CAGT in both R1 and R2: 1073 (10.73%)
```

On `test_files/clock_10K_R{1,2}.fastq.gz`, 8,927 pairs have CAGT in both reads and 1,073 do not (checked independently with `gzip -dc | awk` on bases 9-12). The wording was inherited from Perl 0.6.11 (`trim_galore:389-392`, `:452`), which has the same mismatch.

## Fix

Change the label only:

```
thereof did not have the fixed sequence CAGT in both R1 and R2: 1073 (10.73%)
```

The number, the percentage and the rest of the stderr format are unchanged.

## Testing

- New integration test `tests/integration_clock.rs`: `clock_summary_labels_the_count_of_pairs_without_cagt` runs `--clock` on the clock fixture and asserts `Sequences processed in total: 10000` and the new label with `1073 (10.73%)`. It fails without the fix (the old label is printed).
- `cargo test`: all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

The summary is stderr only. The CI `Validate clock mode` step md5-compares only the two output files (`*.clock_UMI.R1.fq.gz`, `*.clock_UMI.R2.fq.gz`) against Perl 0.6.11, and the other clock CI steps grep for `Clock pair N of M`, `duplicate of pair` and `even number`, none of which change. Output files are byte-identical. The stderr line now differs from Perl 0.6.11 on purpose.

## Suggested CHANGELOG entry

- **The `--clock` summary no longer reports the pairs without CAGT as having it.** The line
  counted read pairs whose fixed sequence was not `CAGT` in R1 or R2 but labelled them "had fixed
  sequence CAGT in both R1 and R2" (wording inherited from Perl v0.6.x), so the clock test data
  showed 10.73% where 89.27% actually carry it. The label now reads "did not have the fixed
  sequence CAGT"; the number and the output files are unchanged.

Part of #546 (finding 14 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52d279be65b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.