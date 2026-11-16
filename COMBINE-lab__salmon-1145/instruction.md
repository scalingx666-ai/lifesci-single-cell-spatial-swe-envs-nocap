# Issue

**Title:** feat(align): warn when a BAM has no usable AS to score by (#1140 PR D)

## Description

PR D of #1140. Deterministic alignment mode without `--errorModel` weights each placement by the BAM's `AS`. A missing tag parses as score 0, indistinguishable from a genuine zero, so a BAM with no `AS` leaves every placement of a fragment tied and the EM apportions multireads by effective length alone. Same exit code, same output shape, quietly worse numbers.

## The cost of staying silent

Same BAM, once as produced and once with the tags stripped, against the truth in the read names (3000-transcript fixture, 300k pairs):

| input | mode | Spearman | MARD |
|---|---|---|---|
| with `AS` | det | 0.92081 | 0.02294 |
| no `AS` | det | **0.76235** | **0.06890** |
| no `AS` | det `--errorModel -t` | 0.90438 | 0.02443 |

Three times the MARD, and the remedy already exists.

## What this adds

Presence is counted where the tag is read, per your note that `record_to_frag` maps a missing `AS` to 0: by the time scores exist, absent and zero are the same number. Each worker tallies `(records, records_with_AS, min, max)`; the tallies merge alongside the existing summary reduction.

Three states draw a complaint, each naming `--errorModel -t` as the way out:

- no record carries `AS`
- some records carry it and some do not, so zeros compete with real scores
- every record reports the same value

The third is why the count is per record rather than per placement, as you suggested optionally: a proper pair sums to twice an orphan's score, so a BAM whose every record says `AS:i:100` looks varied if you judge the sums.

Observed on the three fixtures:

```
with_as   (no warning)
no_as     no alignment in this BAM carries an AS tag (890098 records read): scoring falls back to
          equal weights for every placement of a fragment, so multireads are apportioned by
          effective length alone; pass --errorModel with -t <transcripts.fa> to score the
          alignments from their own bases instead
const_as  every alignment in this BAM reports the same AS (100): [same advice]
```

## Scope

The error-model path never reads `AS`, so it says nothing (structurally: the tally only exists in the branch that scores by the tag). Genome projection goes through `project_genome_bam_to_rad` and scores by bramble similarities, so it is untouched, per your exemption.

## Testing

The verdict is returned on `AlignRadSummary` as well as logged, so the tests assert on a value rather than capturing log output. Five cases in `crates/salmon-align/tests/deterministic_bam.rs`: absent, constant, partial, varying (silent), and the error-model path (silent). The existing fixture in that file carries no `AS` at all, which is how the absent case gets a realistic input for free.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c498cbf07244`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.