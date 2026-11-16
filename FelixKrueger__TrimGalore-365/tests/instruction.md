# Issue

**Title:** fix(cli): distinguish mixed FASTQ+BAM pairs from two-BAM pairs

## Description

Fixes the misleading rejection reported in #363, and moves the check into input validation so a guaranteed-to-fail run stops before doing any work.

. (Not `Closes` — this targets `dev`, where auto-close does not fire; #363 needs a manual close after merge.)

## The reported defect

Two sites looped over a `--paired` pair and bailed on the **first** BAM found, so any pair containing at least one BAM got the two-BAM message:

```console
$ trim_galore --paired sample.fastq sample.bam
Error: --paired with two BAM files is not supported. … Got two BAM files;
       one of them is sample.bam.
```

Only one input is a BAM, so both statements are false — and the remediation it offers (pass a single interleaved BAM) is not what the user wants: the cause is usually a mis-typed filename, or an intent to pass two FASTQ files.

## After

| Input | Message |
|---|---|
| one BAM in the pair | `--paired requires both inputs of a pair to be the same format. Got mixed: A is FASTQ (plain) and B is uBAM. Pass two FASTQ files, or a single interleaved uBAM. If you meant two FASTQ files, check for a mis-typed filename.` |
| two BAM files | existing message, now naming **both** files, plus a verified combine command |
| `--clump_only`, FASTQ output | unchanged — uBAM input there requires `--output-format ubam`, because the FASTQ path would drop aux tags |

## Two things the issue got wrong

**`main.rs:543` was not a third cause site.** It already branched two-BAM vs mixed correctly and had regression coverage, so it was the *reference implementation* for this fix. It is now redundant and removed.

**"Diagnostic quality only" understates it.** On the trimming path the check sat *inside* the per-pair worker, so before the error appeared a rejected run had already auto-detected adapters over up to 1 M reads per input, printed the banner, created `--output_dir`, and — on multi-pair input — **fully trimmed and written every pair preceding the offending one**, including their `_val_{1,2}.fq.gz` files and trimming reports. A pipeline consuming whatever pairs succeeded now gets nothing. That is a real behaviour change and is called out in the CHANGELOG.

## Design

One guard, `format::reject_bam_format_mismatch_in_pair`, dispatched by a `PairedShape` enum and called once from `main()` beside the `--phred64` guard — it consumes the `input_formats` vector already computed there, so it needs no I/O. It runs ahead of `ensure_output_dir`, all three output-collision pre-flights, and every dispatch branch.

Three points worth flagging for review:

1. **The predicate is a BAM *count*, not format equality.** `InputFormat` has three variants and a plain+gzip FASTQ pair is legal. Naming the helper for "mismatch" invites `formats[0] != formats[1]`, which breaks a working invocation — pinned by a test.

2. **`--clump_only` with FASTQ output is asymmetric by design**: it rejects on *any* BAM in the pair, not on disagreement, because there the problem is BAM-on-a-FASTQ-path whether one input or both is a BAM. The actionable information is a flag, not a re-shaped input. The first draft of this fix got that wrong and would have printed `trim_galore --clump_only --paired interleaved.bam` — a command the binary itself rejects. That path had zero coverage; it does now.

3. **Three call sites keep an *enforced* internal-invariant check, not a comment.** `run_paired`'s sequential `--cores 1` path (the default) hard-codes `FastqReader::open`, and a BGZF BAM handed to `FastqReader` parses as FASTQ rather than erroring. The two two-file leaves take the source header from R1 alone, so any BAM reaching them is silent wrong output — a mixed pair blends FASTQ-derived and BAM-derived records, a two-BAM pair discards R2's `@PG` chain. Hoisting a guard converts local invariants into one remote one, so the leaves assert rather than document.

## Remediation verified, not inferred

The two-BAM message now names a command that combines two files. The obvious candidate is wrong in a dangerous way: `samtools collate -O r1.bam r2.bam` **exits 0 having written only r1's records**, because `collate`'s second positional is the temp-file prefix. Measured on samtools 1.21 — 10 000 of 20 000 records, no warning. The message uses `samtools merge -n`, verified end-to-end to produce a mate-adjacent file TrimGalore accepts.

## Also in this change

- Retires an already-unreachable check in the `--clump_only` uBAM N=1 branch (its condition was a strict subset of `main()`'s N=1 guard).
- Promotes `input_format_label` out of `clump_only.rs`, so error text never shows internal enum names (`FastqGz`, `UnalignedBam`).
- Corrects `docs/quickstart.md`, which stated paired reads "may come as two BAM files" — the binary rejects that. Verified it was the only such claim across `docs/src` and `README.md`.

## Scope

Unchanged for `--hardtrim5/3`, `--clock` and `--implicon`. `--hardtrim5/3` never consult `--paired`, so a mixed pair is genuinely harmless there; `--clock`/`--implicon` do pair and currently report a misleading read-count error whose firing is incidental on record counts. Tracked in #364 rather than folded in, since the two mode groups need opposite decisions and applying uniformity would remove working invocations for no correctness gain.

## Verification

- **Tests 421 → 441** — 9 unit tests in `format.rs`, 11 integration tests in the new `tests/integration_paired_format_guard.rs`.
- The three pre-existing rejection tests pass **unedited** (`git diff tests/` empty for them) — their loose substring assertions were a design constraint on the new wording, not something to update.
- `cargo fmt --all -- --check` and `cargo clippy --all-targets --release -- -D warnings` clean.
- **Byte-identity against Perl 0.6.11 confirmed unmoved** on all five CI matrix paths (SE, PE, hardtrim5, clock, demux) plus `--clump_only`, by md5-comparing 15 outputs against a build of `dev` @ `a4ffd47` in a separate worktree.
- Reviewed by two independent code reviewers and a coverage audit before this PR: 4 defects found and fixed, 5 recommendations adopted. The most serious was a CHANGELOG paragraph asserting a bug that never shipped — it claimed the old message suggested the destructive `collate` form, which it never did; that form existed only in a plan draft. Full record in `plans/mixed-format-pair-message/PLAN.md` §14.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4ffd471d4d5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.