# Issue

**Title:** docs(cli): make --clump_only's help text format-aware

## Description

`--clump_only`'s `--help` text predated the shipped uBAM arms: it listed `--output-format ubam` among the *rejected* flags and closed with "v1 is FASTQ in / FASTQ out only", so it actively deterred users from a feature that works. Reviewing the whole block turned up five falsified claims rather than the two the issue named, and the worst was the output-filename sentence — FASTQ-only and unqualified, while a paired run under `--output-format ubam` writes **one** interleaved `*_clumped.bam`, not two mate files. That sentence sits in paragraph 1, which is the only paragraph clap renders for `-h`, so fixing just the two named sentences would have left short-help users both uninformed and misdirected.

The block is now format-aware throughout: per-format output filenames, `--compression` and `--dont_gzip` marked FASTQ-output-only, `--preserve-tags` named as the aux-tag opt-in (so "lossless" isn't read as covering tags that silently drop without it), the appended `@PG` record noted as why whole-file identity doesn't hold on BAM output, and uBAM input documented as *requiring* `--output-format ubam` rather than being one of two options — the FASTQ output path refuses it. The `--output-format ubam` value description also gained the two rejections it was missing (`--retain_unpaired`, `--dont_gzip`).

No behaviour change. Filename claims were smoke-tested rather than assumed: SE gives `R1_clumped.bam`, PE gives exactly one `_clumped.bam`, and `--dont_gzip --output-format ubam` is rejected as the new copy describes. 561 tests green.

<details>
<summary>AI-assisted: plan, dual plan review, and what they corrected</summary>

Plan + reviews in `plans/08082026_clump-help-text/` (committed separately). The original plan scoped this as the issue's "two-line fix"; both reviewers rejected that, and both caught that its own proposed copy would have introduced two *new* falsehoods — appending `--output-format ubam` to a "Composes with" list that already contained `--dont_gzip` (a hard error together), and "FASTQ and uBAM are both supported on input and output", which implies four legal combinations when only three exist. Reviewer B's empirical finding that `-h` renders only paragraph 1 is what put paragraph 1 in scope.

Maintainer decisions: no docs-site pointer (it would be the first in any `cli.rs` help string, and the changelog records deliberately removing unresolvable pointers from flag descriptions), so the two paired shapes are stated inline; and the `OutputFormat::UBam` variant doc was folded in rather than deferred.

Historical changelog records carrying the same stale wording are release history and deliberately untouched.
</details>

 (manual close needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac08a97025bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.