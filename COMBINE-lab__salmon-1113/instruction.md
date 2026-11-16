# Issue

**Title:** perf(map): drop the per-fragment and per-call maps from the hot paths

## Description

Part of #1085 — its map-side half. The quant-side half landed with #1099.

**This is the first change out of this audit with an unambiguous end-to-end win.** 10M human fragments, reads path, `-p 16`, interleaved, warm-up discarded:

| | mean | sd |
| --- | --- | --- |
| develop | 28.845 s | 0.317 |
| this PR | **28.156 s** | 0.218 |

**−0.689 s (−2.39%), t = −5.28**, 95% CI −0.950 … −0.428, faster in **9 of 9 rounds**. Worth stating against the run of nulls in #1092: every other structural item measured |t| ≲ 2 with a CI straddling zero. This one does not.

It is also the size the microbenchmark predicts — dedup runs once per fragment, and at typical n the scan is 7–8× faster than allocating a map (8.2 ns vs 61.0 ns at n=4); ~50 ns × 10M ≈ 0.5 s.

## What changed

**Deduplicating raw mappings by transcript** allocated an `AHashMap` per fragment to handle what is typically 1 to 20 entries. Now a hybrid, split at the measured crossover:

| n / distinct | AHashMap | prefix scan | reused table |
| --- | --- | --- | --- |
| 4 / 4 | 61.0 ns | **8.2** | 38.5 |
| 20 / 12 | 231.5 | **29.1** | 104.7 |
| 60 / 30 | 513.9 | **173.6** | 270.4 |
| 100 / 50 | 851.9 | **399.7** | 429.3 |
| 128 / 64 | 1325 | 752.3 | **586.7** |
| 160 / 80 | 1439 | 1004.5 | **591.5** |

`DEDUP_HASH_THRESHOLD = 112`, the midpoint of the crossing interval, with a `const` assertion that it stays in a range where both paths are reachable in a real run.

**`best_per_target`** allocated an `AHashSet` per call; it now scans the kept prefix in place, preserving both the survivor and the highest-coverage-first ordering.

## The part that took two attempts

The tie rule is load-bearing. The map replaced an entry only on a **strictly** greater score, so among equal scores on one transcript the first in arrival order survived — and those records carry different positions, so a different survivor shifts the fragment's bias and fragment-length weights.

My first attempt sorted by `(tid, score, ref_pos)`. Every `sample_data` check passed, and it **silently changed 55 equivalence classes** on 10M human fragments (407,855 vs 407,800) — small enough to miss, large enough to matter. Only the human-scale byte comparison caught it.

Both paths now apply the original rule, with a test asserting they agree on cases loaded with ties, negative-controlled by flipping the table path to `>=` (fails on a 2-mapping case).

Conversely the survivors' *order* is **not** part of the contract, which is worth recording: the map being replaced was seeded per process (`ahash` `runtime-rng`), and develop is byte-identical across separate runs regardless, so the order it yielded cannot be load-bearing.

## Scratch, not thread-local

`DedupScratch` is threaded through 4 signatures rather than held in a `thread_local`. On 200 mappings:

| | |
| --- | --- |
| threaded parameter | **768 ns** |
| `thread_local` | 839 ns |
| fresh allocation per fragment | 1468 ns |

Reuse is what matters most — allocating on demand is 1.9× worse — and the parameter recovers the remaining ~10% that the lazy-init check and `RefCell` borrow cost (a `HashTable` has a `Drop`, so a bare const-init TLS is not available). `QuantProcessor` already owns a `RecordScratch` from #1099, so it has a natural home; the two convenience wrappers that allocate their own `out` allocate a scratch too, which costs them nothing relative to what they return.

Hashing is `ahash` with fixed seeds. `hashbrown::HashTable` takes the hash from the caller and has no default hasher, so `std`'s SipHash is not reachable here.

## Verification

- `quant.sf` **byte-identical** to develop on 10M human fragments (407,800 eq-classes, 9,221,625 mapped)
- byte-identical on `sample_data` across plain / `--seqBias --gcBias --posBias` / `--softclip` / `--sketch`
- full suite, `clippy --workspace --all-targets -D warnings`, fmt clean

## Not touched

`cfg.chain.clone()`, which #1085 lists among "4 or more Vecs per fragment". `ChainConfig` is `{i32, i32, f32, usize}` — a ~24-byte POD copy, not heap traffic. Same false positive as the `PiscemStreamingQuery` item already withdrawn in that issue.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YKxqH6k1sbmDC1bpNso3zr

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3db9c1271359`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.