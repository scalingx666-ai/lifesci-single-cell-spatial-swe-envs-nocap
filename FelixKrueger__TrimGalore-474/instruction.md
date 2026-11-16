# Issue

**Title:** fix(clump): bound the per-record cost that size_of cannot see

## Description

`--clumpify` charged the bin pool per byte while part of its cost is per record, so short reads exceeded the memory peak the binary printed — 1.16–1.30 of prediction at 25 bp. The sizing coefficients now bound that breach at the shortest calibrated read length (`23·n_bins + 64·cores` → `33·n_bins + 92·cores`), which makes bins ~30% smaller at every budget, moves output bytes again (same records, different gzip member boundaries), and raises the minimum viable `--memory` — `--fastqc` above `--cores 23` now falls back to plain trimming at the default 1G. Worst rep of three per cell on darwin/arm64: 25 bp c8/2G 1.300 → 0.927, c2/1G 1.201 → 0.838, c4/1G 1.161 → 0.816. Both 25 bp CI cells now gate on `peak ≤ prediction`; the baseline is deliberately left in `BOOTSTRAP` because its committed centres are pre-refit, so **the first CI run here supplies the real ones**.

.

<details>
<summary>Why the coefficient is a bound rather than a fit (AI-assisted analysis)</summary>

`size_of` accounts for 148 B of a paired slot and that part is exact — it is now pinned by a `const` assert. But a slot costs **245–270 B**: the three `String` allocations per record each carry ~20 B that neither `size_of` nor `estimated_record_bytes` can see. That excess is allocator-independent (libmalloc and mimalloc agree within 1–4 B/pair), page reuse means it does not accumulate across flush cycles, and it is *not* attenuated by bin occupancy. It also varies ~10% across read lengths, so **no per-record constant is exact at more than one read length** — which is why this bounds the measured breach instead of modelling it.

The scale factor is `(peak − static) / (prediction − static)`, which moves only 1.331–1.349 across a 173–260 MiB range of `static` — so it does not rest on the one term this design cannot identify. Both terms scale together because the calibration matrix holds only two `n_bins:cores` shapes and cannot separate them.

Also included:

- The reservation follows the previous flush cycle's mean rather than whichever record arrives first after it, so one short record cannot size a whole cycle. 6% headroom, because landing one slot short costs a full `Vec` doubling — ~half of cycles on variable-length input, and invisible to every fixture here because they are all fixed-length.
- Reads below the 25 bp calibration floor warn. The floor is a **read length, not a record size**: header bytes raise the per-record size and so make a run safer. Every input is checked, so a multi-pair run cannot hide a short pair behind a long first one.
- The drift band narrows `0.09` → `0.065`. Lever A is one extra whole bin per worker, so its magnitude in ratio-of-prediction units is proportional to `B` and falls with it; at `0.09` the band would have been *wider* than the regression it exists to catch.

**Outstanding, and needs CI rather than a laptop:** the Linux cells (rule is take the worse of the two), the post-refit lever-A delta measured rather than inferred, and an output-size measurement on a library with duplicates — the calibration fixture is 100% distinct sequences and cannot show a clumping gain or its loss, so no compression cost is claimed in either direction.

One thing to watch on the CI run: the c2 cell's relative within-cell spread roughly doubled post-change (2.3% → 4.98%). That is still inside the 5.55% the margin rule assumed, but that figure was derived pre-change. If Linux shows the same widening, the margin's input wants re-deriving from post-change data.
</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3fa4de3b3c8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.