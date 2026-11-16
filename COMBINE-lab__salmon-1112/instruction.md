# Issue

**Title:** fix(infer): widen CSR offsets to u64 and drop the incidence ceiling

## Description

.

## What is at risk, and what is not

`starts` holds cumulative *incidence* counts, so it grows with the whole dataset. Everything else in `PackedEqClasses` is safe: `labels` holds transcript ids (bounded by `num_txps`), `combined`/`weights` are already `f64`, `counts` is already `u64`, and the remaining `u32`s in the crate are user-specified iteration and sample counts. I checked the rest of the workspace for the same cumulative-cast shape — `starts.push(labels.len() as u32)` was the only instance.

So the fix is one field, one entry per class.

## Why widen rather than select the width

#1097 planned to choose `u32` or `u64` from the incidence count, rejecting a blanket widening as "real memory on a large index". The numbers do not support that:

| eq classes | `starts` u32 | u64 | delta | delta as % of packed |
| --- | --- | --- | --- | --- |
| 411,419 (our human run) | 1.6 MB | 3.3 MB | 1.6 MB | **3.45%** |
| 1,000,000 | 4.0 MB | 8.0 MB | 4.0 MB | 3.45% |
| 10,000,000 | 40 MB | 80 MB | 40 MB | 3.45% |
| 100,000,000 | 400 MB | 800 MB | 400 MB | 3.45% |

A flat ~3.5% of the packed structure at every scale — 0.155% of peak RSS on the human run. And the regime the narrow width protects is unreachable: `u32` overflows past 4.29 B incidences, ~859 M classes at k=5, whose `starts` array is **already 3.4 GB as `u32`**, with ~86 GB of labels and weights beside it.

Against that, the selection machinery is an enum or a generic parameter — the latter propagating through `optimize`, `optimize_with_init`, bootstrap/Gibbs and the RAD path, as #1097 itself notes. A one-word type change does the same job.

## The cost, measured

Interleaved A/B of the EM phase on the 10M-fragment human RAD, warm-up discarded. The point estimate drifts down as rounds accrue and the sign is barely better than a coin flip:

| n | delta | t |
| --- | --- | --- |
| 11 | +1.62% | 1.80 |
| 20 | +1.40% | 2.07 |
| 27 | +1.10% | 2.06 |
| **29 (all rounds)** | **+0.95%** | **1.86** |

At the full sample: `u32` 11.782 s (sd 0.341), `u64` 11.894 s (sd 0.289), 95% CI `-0.009 .. +0.232 s` — spanning zero. `u64` is slower in **16 of 29 rounds**, i.e. 55%.

So: a point estimate near +1% that this benchmark cannot separate from noise. Not a demonstrated regression, and not a demonstrated absence of one either — if there is a real effect it is below what ~30 rounds at this variance can resolve. The plausible mechanism (doubling an array read once per class per iteration) argues for taking the ~1% as an upper bound rather than assuming zero.

`quant.sf` is byte-identical between the two builds.

## Acceptance criteria

- [x] Inputs above `u32::MAX` incidences quantify rather than asserting
- [x] The #1094 assertion is removed
- [x] EM-time effect reported rather than asserted (above)
- [x] `quant.sf` byte-identical between the two builds
- [n/a] "Offset width selected from the incidence count" and "a test exercises the `u64` path" — both moot once there is only one path; the `u64` path is now the only one, so every existing test exercises it

Full suite, clippy `-D warnings` and fmt clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YKxqH6k1sbmDC1bpNso3zr

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `87cbb1a70a15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.