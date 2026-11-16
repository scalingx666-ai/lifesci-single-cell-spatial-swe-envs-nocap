# Issue

**Title:** fix(cli): auto-create -o/--output_dir if missing (was hanging)

## Description

## Summary

Reported via beta.5 user feedback: a SLURM-cluster paired-end run with \`-j 10 -o ../outdir\` against plain-text \`.fastq\` input hung at **4 seconds CPU after 24 hours wall** when \`../outdir\` didn't exist beforehand. User confirmed re-running with the directory pre-created succeeded in ~7 minutes.

## Root cause

\`src/fastq.rs:430-436\` (single-threaded \`FastqWriter::create\`) creates the parent dir lazily — but \`src/parallel.rs:179-182\` (parallel paired-end path) opens outputs via raw \`File::create(...)?\`, which fails immediately on a missing parent. By that point reader and worker threads have already been spawned upstream. The \`?\` exit drops the receiver channel; workers stay stuck producing into a queue with no consumers; deadlock at near-zero CPU.

## Fix

New \`io::ensure_output_dir\` helper called from \`main()\` immediately after CLI parse, before any threads are spawned. Single choke-point covers every downstream code path:

- parallel paired-end (the originally-broken one)
- single-threaded paired-end
- single-end (any cores)
- \`--hardtrim5\` / \`--hardtrim3\`
- \`--clock\` / \`--implicon\`
- \`--demux\`

Restores Perl v0.6.x behaviour: *"If an output directory which was specified with -o output_directory did not exist, it will be created for you"* (v0.6.0 changelog).

## Tests

3 new \`io::tests\` covering the three cases:
- \`creates_missing\` — \`Some(nested non-existent path)\`, asserts created
- \`idempotent_on_existing\` — \`Some(existing path)\`, called twice
- \`none_is_noop\` — \`None\` passes through cleanly

Total test count: **165 → 168**. \`cargo fmt\` clean, \`cargo clippy --all-targets --release -- -D warnings\` clean.

## Test plan

- [x] \`cargo test --release ensure_output_dir\` — all 3 pass
- [x] \`cargo test --release\` — 168 passed, 0 failed
- [x] \`cargo fmt --all -- --check\` — clean
- [x] \`cargo clippy --all-targets --release -- -D warnings\` — clean
- [ ] CI on this PR
- [ ] Manual smoke (post-merge): \`trim_galore --paired -j 4 -o /tmp/nonexistent_$(date +%s) test_files/BS-seq_10K_R1.fastq.gz test_files/BS-seq_10K_R2.fastq.gz\` should now succeed instead of hanging

## CHANGELOG

Queued for v2.1.0-beta.6 (top of the existing \`Bug fixes (since v2.1.0-beta.5)\` list — feels appropriate to surface this loudly given it's a deadlock not a cosmetic bug).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a28141e061bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.