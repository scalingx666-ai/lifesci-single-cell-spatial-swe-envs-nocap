# Issue

**Title:** fix(quant): derive MAPQ from the placement count instead of a constant 1

## Description

The MAPQ half of #1141, as its own PR per your review, fully decoupled from realization: no re-alignment, no `ambiguous.bin`, no new index artifact. The count of placements is already in hand when the records are written, so this is arithmetic on a value the writer holds.

## What changes

Every record carried `MAPQ 1`, which says "probably wrong" about placements salmon chose to keep. `samtools view -q 255`, the standard "uniquely placed" filter and the one STAR output trains people to use, therefore discarded the whole file.

salmon has no phred-scaled probability to offer, and this does not invent one. It reports what salmon does know, on the scale STAR already established:

| placements (`NH`) | `MAPQ` |
|---|---|
| 1 | 255 |
| 2 | 3 |
| 3 or 4 | 1 |
| 5 or more | 0 |

On a 300k-fragment fixture (890098 records):

```
before   890098 records at MAPQ 1;      -q 255 selects 0
after    433027 at 255, 199088 at 3, 168502 at 1, 89481 at 0;   -q 255 selects 433027
```

## Docs

The output-formats page gains a short `MAPQ` section stating the scale and, more importantly, that a salmon `MAPQ` counts placements rather than estimating a probability. That belongs in the pseudobam contract paragraph you are landing for 2.6.0; treat this as a first draft of that one field's entry and fold it in if it fits better there.

## Scope

Unit test for the scale, including the boundary at four placements and the `nh == 0` case a record built without a placement would hit. Full workspace suite green, clippy and fmt clean. Nothing else from #1141 is here.

I have taken the rest of your review as written: #1141 and #1142 wait for the opt-in design discussion after 2.6.0, and the scoring-path question goes to its own issue with the fixtures, which I am putting together now. I do want to answer one substantive point there rather than here, since it changes what the issue should measure: the anchor pathologies were found by the realization DP, but the reason I think they are worth chasing is that the *positions* they disagree with come from the same chaining that feeds scoring. Whether that disagreement reaches the scores is exactly the open question, and I would rather measure it than assert it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4b259db18a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.