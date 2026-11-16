# Issue

**Title:** fix(report): accumulate bp_after_cutadapt on the parallel path

## Description

`Total written (filtered)` moved with `--cores`. On `--clip_R1 5` over `BS-seq_10K_R1.fastq.gz` the cutadapt section reads 644,525 bp (99.2%) at `--cores 1` and 594,545 bp (91.5%) at `--cores 4`; on `--rrbs`, 490,527 against 483,967. The trimmed records are byte-identical either way, so this is the report alone — but `--clumpify` requires `--cores >= 2`, which makes every clumpify run one of the affected ones.

The parallel path added the final record length to `total_bp_after_trim`, where the serial paths add `TrimResult::bp_after_cutadapt` — the post-adapter length captured before RRBS, poly-X, N-trimming and clipping, which #232 introduced so the section reports what Perl v0.6.x's cutadapt subprocess wrote rather than what the wrapper went on to truncate.

It is an orphaned call site rather than a dropped fix. 82d1e34 wrote the three parallel sites correctly in April, when `bp_after_cutadapt` did not yet exist; f4b544d created it a fortnight later, switched the serial sites, and touched no line of `parallel.rs`. That commit's own message says it applies the new quantity "in both single-end and paired-end pipelines", which has not held for `--cores >= 2` since.

Two tests already compared serial and parallel `TrimStats` — the single-end one, and less obviously `test_passthrough_serial_parallel_parity`, which asserts both R1 and R2. Both were vacuous for this field, because `parity_test_config()` disables every post-adapter stage and `bp_after_cutadapt` then equals `seq.len()` by construction. The two new tests clip both reads at both ends and assert hand-derived absolute totals (960 single-end, 960 and 990 for paired R1 and R2) rather than only `serial == parallel`, since a change flipping the *serial* line would otherwise keep the suite green and revert #232 in silence. Each also asserts that its fixture still discriminates, so a later fixture edit cannot quietly restore vacuity.

Four mutants, all caught: reverting `:542` fails on R1, `:543` on R2, `:1157` single-end, and flipping the serial and parallel single-end sites together passes the parity assertion and trips only the absolute anchor. The CI validation matrix runs `--cores 1`, so it stays green whether or not this is fixed — these tests are the whole guard.

844 tests, `clippy --all-targets --release -D warnings` clean, `fmt --check` clean. Paired reports verified stable across core counts (R1 644,525, R2 645,073), trimmed output byte-identical to pre-fix, and JSON `basepair_processing.total_bp_written` unchanged at 594,545 throughout.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0bbee442b16`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.