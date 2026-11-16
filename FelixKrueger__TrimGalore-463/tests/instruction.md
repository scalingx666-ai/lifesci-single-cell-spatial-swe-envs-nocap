# Issue

**Title:** fix(cli): count the --rrbs auto-clip in the --rename uBAM guard

## Description

.

`--rrbs --paired --rename --output-format ubam` with no clip flag ran to completion and silently dropped the annotation. The #408 guard counted only the clip flags on the command line, but the directional paired path auto-sets `--clip_R2 2` *after* the guard runs — so a clip did apply, `--rename` did append `:clip5:` to Read 2, and the BAM QNAME kept only the first whitespace-delimited token. It is now refused, like every other shape where the annotation cannot survive.

<details>
<summary>Verification detail (AI-assisted)</summary>

**Observed, not derived.** #459 was written from reading the code path; both the issue and the review that found it flagged the final step as unverified. On a 40 bp pair with a description in the header, the output R2 record is **38 bases** with QNAME `readone` and no `:clip5:` anywhere — exit 0, no warning. After this change the same command exits 1 with the #408 refusal and writes nothing.

**One predicate, two consumers.** `Cli::rrbs_sets_clip_r2()` is now the single spelling of `rrbs && !non_directional && paired`; the guard and `setup_trimming` both read it. Open-coding it in the guard would have added a seventh site encoding when a Read 2 clip applies, which is the duplication #450's fold-in was reducing.

**The three shapes where the auto-clip does not fire stay accepted**, each a row in the new test table: `--non_directional` (skips the auto-clip), single-end (the auto-clip is paired-only), and FASTQ output (unaffected, and still logs the auto-clip).

**Mutations, in opposite directions.** Dropping the guard term loosens it and turns the should-refuse row red (1 failure); making the predicate ignore `--non_directional` tightens it and turns the should-run row plus the unit test red (2 failures). A mutation that loosens a condition cannot turn a should-succeed test red, so the pair opposing each other is what makes them meaningful.

798 tests (2 new), `fmt` and `clippy --all-targets --release -D warnings` clean. No file in the clumpify memory path is touched, so the peak-RSS baseline is undisturbed.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `51fa55e6a6af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.