# Issue

**Title:** fix(align): detect a single-end BAM and its strand under -l A on the RAD paths

## Description

## Problem

The default `-a` path (`write_alignment_rad`, and `project_genome_bam_to_rad` for genome BAMs) treated a single-end BAM under `-l A` as paired. It decided pairedness from the text of `-l`, and `A` is not one of `U`/`SF`/`SR`/`S`. Only proper pairs fed the format tally, so a single-end read gave no strand evidence. Two wrong results follow.

**`--discardOrphans` empties the run.** Every single-end placement has one record, so the orphan rule drops it. Measured on a 300-read fixture on this branch's base:

| `-l A --discardOrphans` | `num_mapped` |
|---|---|
| before | 0 |
| after | 300 |

The audit measured the same on a larger BAM: 0 under `-l A`, 2000/2000 under `-l U`.

**A stranded library is quantified as unstranded.** No format is detected, so no strand filter applies. From the audit's run, with 500 antisense-only reads on `txB`:

| | `txB` count | `detected_library_type` | `frag_length_source` |
|---|---|---|---|
| `-l A`, before | 500 | `null` | `alignments` |
| `-l SF` | 0 | `SF` | `prior` |

The audit also saw class weights move (0.9977/0.0023 versus 0.877/0.123). `alignments` is wrong because a single-end run measures no fragment lengths: the baked distribution is the `--fldMean`/`--fldSD` prior.

`--online` did not have this problem: it already peeks at the first record.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit spotted that the online and RAD paths derive pairedness differently, then reproduced it by running both library types on small synthetic BAMs. The numbers above come from those runs and from the new tests. Tracked in #1283 (finding 2).

## Fix

- `rad_library_is_paired` (`salmon-align/src/lib.rs`): under `-l A`, reuse `peek_alignment_is_paired`, as the online path does. Both RAD writers call it, so the RAD header and the orphan guard are right.
- `DiscreteFld::add_single_end`: tally the strand of each uniquely-mapped single-end read. `finish` picks single-end inference when those reads are the majority. It is an integer tally, so it stays independent of thread order.
- Both writers feed that tally. On the genome path the strand is the existing transcript-relative one.

The existing baking then gives the right result: `SF`/`SR`/`U` lands in the RAD, the reader filters on it, and the FLD is reported as `prior`.

## Behaviour changes

- An explicit `-l` on a single-end BAM now also bakes the measured format, as paired runs already do. So `detected_library_type` is filled in, and `library_type_mismatch` can now fire on such a run. The filter still follows the explicit `-l`.
- The peek reopens the input. The writers already open it separately to read the header, so a FIFO was not usable on this path before either.

## Limits

Pairedness comes from the first record, like `--online`. In a mixed BAM starting with a paired record, `--discardOrphans` still drops the single-end reads. An explicit paired `-l` on a single-end BAM is unchanged.

## Verification

- New tests in `crates/salmon-align/tests/deterministic_bam.rs`. I saw all three fail without the fix (`0` versus `300`, `null` versus `"SF"`):
  - `-l A` gives the same counts, `num_mapped` and `frag_length_source` as `-l SF`, and detects `SF`.
  - `--discardOrphans` under `-l A` keeps all reads.
  - A genome BAM with a plus and a minus transcript detects `SF`.
- `salmon-align`, `salmon-model` and `salmon-cli` tests pass, and workspace clippy is clean with `-D warnings`. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.