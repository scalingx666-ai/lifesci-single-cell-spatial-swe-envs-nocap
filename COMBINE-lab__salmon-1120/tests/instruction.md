# Issue

**Title:** perf(quant): reuse positional-bias buffers across transcripts

## Description

Addresses the positional-bias allocation item in #1091 — the last item there triaged as *address*.

### Change

The bias-corrected effective-length pass allocated **six `Vec<f64>` per transcript** inside its `par_iter` over the whole transcriptome: four for the projected 5'/3' obs/exp densities, plus two more returned by `positional_factor`. On a human index under `--posBias` that is roughly 1.5M transcript-length-sized allocations per correction round.

`map_init` now gives each rayon worker one `PosScratch` to refill, so the count goes from six per *transcript* to six per *worker*. `positional_factor_into` writes into a caller-provided buffer, and `positional_factor` is now a thin wrapper around it — so the two cannot drift apart, and the align-mode caller needs no change.

The four projection buffers are `resize`d to each transcript before use, since `project_weights` derives its output length from the slice it is handed.

### Numerically identical

Verified at `-p 1`, where the pipeline is deterministic:

| run | result |
| --- | --- |
| sample data, `--posBias` alone | `quant.sf` byte-identical |
| sample data, `--posBias --seqBias --gcBias` | byte-identical |
| GRCh38 decoy index (194 decoys), all three bias models | byte-identical |
| 10M human fragments, all three bias models | byte-identical |

The **EffectiveLength** column — what this code actually computes — was also compared on its own, identical in both composed runs.

At `-p 16` that column differs, but this is pre-existing and not attributable here: develop differs from **itself** run-to-run in 186,065 rows, against 189,913 rows across arms. That is the known online-phase threading wobble.

### Performance — null

10M human fragments, `--posBias --seqBias --gcBias`, `-p 16`, interleaved, warm-up discarded:

```
  develop  39.859s
  this PR  39.747s
  delta    -0.28%     paired t=-0.54   95% CI [-0.528,+0.304]s   faster in 5/8
```

Not a win. The allocations are real, but ~1.5M of them amount to well under a second against a 40-second run, and they only occur under `--posBias` at all. I am putting this up because the issue asked for it and it is tightly scoped and provably output-preserving — not on a performance claim. Entirely reasonable to decline it on the grounds that a null result does not justify the churn.

With this, every item on #1091 is either landed, deferred, or rejected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `434ee266ab7f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.