# Issue

**Title:** fix(align): refuse a BAM that is not grouped by read name

## Description

## Problem

`-a` needs the records of each read to be consecutive. A header that says `SO:coordinate` is refused up front, but with `SO:unknown` or no `@HD` line nothing checked the actual order. Each mate then became a fragment of its own, so every count doubled and every fragment looked like an orphan. On `develop`, with 2000 pairs in position order and `SO:unknown`:

```
exit 0
num_processed 4000, num_mapped 4000, num_orphan 4000
NumReads sum 4000
```

The only signal was `no_concordant_mappings`, which suggests checking the pairing but does not name the cause.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit read `coordinate_sorted_unusable`, saw it returns false for a missing or unknown sort order with no check at run time, then ran a generated SAM to confirm the doubling. The numbers above were measured again on `develop` for this PR. Tracked in #1283 (finding 11).

## Fix

A small `GroupingCheck` runs on the reader thread of all three BAM paths: the default RAD writer, genome projection and `--online`. It uses flags only. A fragment is "split" when a mapped record says its mate is mapped too, but the group holds no record of the other segment.

| Share of split fragments | Result |
| --- | --- |
| at least 50% | error, no `quant.sf` |
| 5% to 50% | warning naming the count, and the run continues |
| below 5% | nothing |

Both messages point to `samtools collate` or `samtools sort -n`. On the input above:

```
4000 of 4000 fragments have a mate marked as mapped that is not next to them, so the input is not grouped by read name. Records of one read must be consecutive: group them by name with `samtools collate` or `samtools sort -n`.
exit 1
```

## Choices to review

- **The thresholds are judgement calls.** The warning band exists because a BAM filtered down to one mate can be real, and its flags still say the mate was mapped. A filtered BAM with at least half its fragments in that state would now be refused, with no flag to override. I saw no such case in the tests or the sample data, but it is the main risk here.
- **The check needs the full read.** It fails at the end of the reader pass, after the RAD has been written, not at the start. An early exit after a sample would save time on a big file but miss files that are only disordered further in.

Partly disordered input is the case I did not run: a file with mates apart in only some regions lands in the warning band or below it, depending on the share, and is still quantified.

## Verification

New test: `input_not_grouped_by_read_name_is_refused`, covering `--online` and `write_alignment_rad`. `sample_data/sample_alignments.bam` gives no warning and the same run still produces its `quant.sf`. All `salmon-align` and `salmon-cli` tests and clippy on both crates pass. The whole workspace suite was not run on this branch; CI covers it.

Genome projection gets the same check but has no test of it in this PR.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.