# Issue

**Title:** fix(ubam): honour --phred64 on BAM output; reject it for BAM input

## Description

.

Two coupled `--phred64` defects on the uBAM paths. **They have to land together** — fixing the first without the second introduces a worse, silent one (see *Why one PR* below).

## Bug 1 — silent output corruption (write side)

`BamWriter` subtracted a hardcoded 33 regardless of input encoding, so Phred+64 input was stored under-subtracted by 31: `'h'` (ASCII 104, Q40 at offset 64) was written as raw **71** instead of 40. Because 71 sits inside the SAM-legal 0–93 range, nothing errored — quality was silently inflated for every consumer that reads `QUAL` as raw Phred (samtools, aligners, Bismark).

Affected **all 7** `BamWriter::create` sites — normal trimming, `--hardtrim5/3`, and `--clump_only` — not just the trim path named in the issue. `specialty.rs` was confirmed affected by reproduction, not inference.

Fixed by threading `input_phred_offset` through `BamWriter::create` as a **required** parameter. Deliberately not a defaulted setter: the bug class is *"a call site that never considered the offset"*, so the compiler should force every site to state one. It enumerated 19 edit points, including two a regex pass had missed.

## Bug 2 — total data loss (read side), not in the issue

`BamReader` normalises BAM raw Phred to Phred+33 ASCII, so `--phred64` made `quality.rs` subtract 64 from `+33` data, reducing every score by 31 and discarding effectively the whole library. Reproduced: **10/10 reads "too short", 0 written**.

Fixed by a guard in `main.rs`'s T17 format-dependent validation block. Sited there rather than `Cli::validate()` §3.4a because `validate()` runs *before* input-format detection and cannot see `any_bam` — the same reason §3.4b already lives in `main.rs`. Placed ahead of every dispatch branch (specialty and clump-only both return early) and ahead of `ensure_output_dir`, so a rejected run creates nothing.

## Why one PR

`--clump_only` performs no quality arithmetic, so today's hardcoded `-33` is *correct* on BAM-input paths even with `--phred64` set:

```
--clump_only --phred64 --output-format ubam ubam_test.bam
  input  QUAL md5 = 31878eb2…
  output QUAL md5 = 31878eb2…   identical -> works correctly today
```

Applying the writer fix alone would subtract 64 from the reader's Phred+33 bytes, reducing every score by 31 **while reporting success** — a silent breach of that mode's documented lossless guarantee. The guard is a correctness prerequisite, not a companion. Both plan reviewers proved this independently, and it inverted the original implementation order.

## Also in this PR

- **Read-side overflow.** Unchecked `+` overflowed `u8` for any raw byte > 222. Mixed-sentinel `QUAL` (the all-`0xFF` fast path only fires when *every* byte is `0xFF`) now maps `0xFF` → `'!'` per byte — agreeing with that path rather than diverging — and clamps other out-of-spec values to `MAX_PHRED_SCORE`. Every output byte stays single-byte ASCII, which the byte-indexed `FastqRecord` helpers (`truncate`/`clip_5prime`/`clip_3prime`) require.
- **`PHRED_OFFSET`** (read-side, fixed 33) documented against the new writer field, to prevent exactly the conflation this fix repairs.
- **Startup `NOTE:`** when `--phred64` meets uBAM output, stating that BAM `QUAL` holds true Phred per the SAM spec — the report's `ASCII+64` line describes the *input*, which is otherwise ambiguous sitting next to the BAM.

## ⚠️ Behaviour change

`--phred64` with BAM input is now **rejected in every mode**, including ones where it was an inert no-op and the run worked:

```
trim_galore --clump_only --phred64 <input.bam>
trim_galore --hardtrim5 N --phred64 <input.bam>
trim_galore --phred64 -q 0 <input.bam>
```

Drop the flag — those modes' output is unchanged, and a trimming run now produces the result it should have produced all along. Uniform rather than mode-dependent because a conditional rule ("rejected unless you're in hardtrim, or clump-only-to-FASTQ, or…") is one refactor away from being wrong.

**Archived pre-fix output IS recoverable**, though not in a single invocation. `samtools fastq -n` reproduces the original Phred+64 ASCII verbatim, so:

```bash
samtools fastq -n affected.bam > recovered.fq
trim_galore --phred64 --output-format ubam recovered.fq
```

yields output byte-identical to a correct first run, with no access to the original FASTQ needed.

## Tests

**409 → 421.** New coverage:

| Test | Pins |
|---|---|
`bam_writer_subtracts_input_phred_offset` | offset arithmetic at the raw BAM layer, both branches (cannot compile pre-fix) |
`qual_ascii_conversion_is_single_byte_per_base` | the one-byte-per-base invariant, incl. that byte-indexed slicing doesn't panic |
`phred64_ubam_out_{se,pe_two_file,specialty}_stores_true_phred` | per-writer-family end-to-end wiring |
`phred64_clump_only_ubam_out_stores_true_phred` | clump-only writer |
`phred64_bam_input_rejected_{fastq_out,ubam_out,early_returning_mode}` | guard on all BAM-input routes |
`phred64_clump_only_bam_input_rejected` | the sharpest case — worked correctly pre-fix |
`phred64_mixed_input_rejected` | `any_bam` covers mixed pairs |
`phred64_bam_input_rejected_before_output_dir_created` | guard precedes `ensure_output_dir` |

8 of 9 originally-added tests fail pre-fix; the Phred+33 arm is labelled in-source as an over-correction guard rather than a bug guard.

New fixtures are realistic Illumina 1.5 shape — 24 × `'h'` (Q40) then 10 × `'B'` (Q2), imitating read-segment-quality-control `B`-run tails. A uniform-quality fixture would exercise only one offset *and* trip FastQC's lowest-quality-char encoding heuristic.

## Invariants

- **FASTQ output is untouched**, so the v0.6.11 byte-identity matrix is out of scope by construction.
- **No golden-fixture churn**: nothing in `tests/` or CI passes `--phred64`, `phred_offset()` defaults to 33, and the `assert_ubam_eq` reference BAMs are byte-unmodified.

## Process

Full history in `plans/phred64-ubam/PLAN.md`. Went through dual `plan-reviewer` (both APPROVE WITH REVISIONS — they inverted the implementation order) and dual `code-reviewer` + `plan-manager` (both APPROVE WITH REVISIONS; COMPLETE, 41 DONE / 1 PARTIAL / 0 MISSING).

§14 records what that second round caught, including **one regression I introduced while hardening the read side** (`saturating_add` produced a two-byte UTF-8 char, breaking the byte invariant — strictly worse than the overflow it replaced) and **three false claims in my original CHANGELOG text**, each disproved by measurement rather than argument.

## Follow-ups worth filing separately

- FastQC's encoding heuristic is never appropriate for BAM input — `QUAL` is raw Phred by spec, so any dataset with minimum Phred ≥ 31 reads 31 too low. Pre-existing and upstream-faithful, but this fix moves Phred+64 data from accidentally-correct to affected. An upstream issue against `ewels/FastQC-Rust` would close it.
- `--paired <fastq> <bam>` reports *"two BAM files is not supported"* when only one input is a BAM.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e3da113244d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.