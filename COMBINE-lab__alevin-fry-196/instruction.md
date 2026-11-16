# Issue

**Title:** Cell Ranger-style Hamming-1 UMI correction for cr-like resolution

## Description

## What this does

This PR lets `--umi-edit-dist 1` apply to the `cr-like` and `cr-like-em` resolution strategies. When enabled, `alevin-fry quant` runs a Cell Ranger–faithful per-`(cell, gene)` Hamming-1 UMI correction before the winner-take-all dedup.

The default is unchanged: `cr-like`/`cr-like-em` keep a default `--umi-edit-dist 0` (off), and `trivial` still rejects 1-edit UMIs. Stock code previously **bailed** on `--umi-edit-dist 1` for `cr-like`/`cr-like-em` (`"doesn't currently support 1-edit UMI resolution"`); this PR implements it for those strategies. `--umi-edit-dist` already exists and drives 1-edit correction for the parsimony strategies — this extends it to the CR-mimicking ones.

Two commits:
1. **`feat`** — the faithful Hamming-1 correction (default off).
2. **`perf`** — an output-identical optimization that caps the neighbour scan at the real UMI length.

## Algorithm

`pugutils::correct_umis_cellranger` mirrors Cell Ranger's `lib/rust/tx_annotation/src/mark_dups.rs` (`correct_umis` + `determine_low_support_umigenes`) on `(umi, gene, read-count)` triplets for one cell:

1. **Correction.** For each `(umi, gene)` the destination is the maximum over `{self}` and all Hamming-1 same-gene neighbours, ordered by `(read count, lexicographically larger UMI)`. All destinations are decided simultaneously on the raw counts — one step, no chaining.
2. **Low-support drop.** "Chimeric" keys are found on an intermediate table where each corrected UMI has moved exactly one read to its destination (a Cell Ranger 3 compatibility quirk), then dropped.
3. **Relabel and merge.** Each raw key is relabelled to `(dest, gene)` and merged, so at most one gene survives per UMI and the downstream resolver just counts survivors.

UMIs are 2-bit packed MSB-first with `A<C<G<T`, so integer order equals lexicographic order; a unit test asserts this so the tie-break is well-defined.

## Gating (default off, fail-loud)

| Condition | Behaviour |
| --- | --- |
| `--umi-edit-dist 0` (default for cr-like/cr-like-em) | correction off; stock path, behaviour unchanged |
| `--umi-edit-dist 1` + `cr-like` / `cr-like-em` | correction on |
| `--umi-edit-dist 1` + `trivial` | rejected (unchanged) |
| `--umi-edit-dist 1` + `--sa-model prefer-ambiguity` | rejected (`main.rs`) |
| `--umi-edit-dist 1` + USA mode (3-column tg-map) | rejected (`quant.rs`) |

The two rejections are fail-loud: the correction operates on raw gene ids, which in USA mode are spliced/unspliced/ambiguous variants, so it bails rather than silently mis-correcting (USA mode is auto-detected from a 3-column tg-map, so the guard sits at detection, not on the `--usa` flag). When the correction is on, the tiny-cell fast path is disabled (`--small-thresh` forced to 0) so every cell reaches the corrected resolver instead of the exact-dedup fast path that would bypass it — and that override is now **logged** (previously it would have silently overridden a non-default `--small-thresh`).

## Performance — UMI-length-capped scan (commit 2, output-identical)

The step-1 neighbour search scanned a fixed 32 base positions per UMI (96 hashmap probes), but real UMIs are much shorter (12 bases for 10x Flex); positions at/beyond the true UMI length can never hit a stored UMI, so ~60 of those 96 probes are guaranteed misses. The `perf` commit threads the UMI length in bases from the RAD file-level `"ulen"` tag (the chemistry declaration written at mapping time from the geometry string — the same source `convert.rs` reads, **not** inferred from data) and caps the scan at `0..umi_len` — 36 probes instead of 96 for Flex.

**Output-identical** (the removed probes never matched). Verified on 40k_DTC: the ON count matrix is byte-identical to the un-capped ON matrix (dims, total UMI, barcode/gene sets, per-gene sums, and the order-independent mapped-triplet hash all match), while the `alevin-fry quant` phase wall dropped **70.5 s → 52.6 s** (n=1 cold). A `debug_assert!(umi_len <= 32)` guards the u64-packing shift invariant.

## Impact — results, benchmarking, profiling (measured)

Measured on five 10x Flex datasets (probe references, `cr-like`, 32 threads, min-of-3 timed reps from a controlled cold cache), correction **OFF (`--umi-edit-dist 0`) vs ON (`--umi-edit-dist 1`)** with the same binary.

**Results (counts).** OFF is byte-identical to the stock `cr-like` reference on all five (the feature is inert by default). ON reduces total UMI as Hamming-1 duplicates collapse into their higher-support neighbour; non-zeros barely move (the collapse merges within a gene, it doesn't drop genes):

| Dataset | total UMI OFF → ON | Δ% | Δ nnz | OFF vs stock |
| --- | --- | ---: | ---: | --- |
| Flexv2_16k_Human | 141.6M → 136.4M | −3.64% | −5,355 | identical |
| 16k_mouse_Spleno | 241.4M → 232.7M | −3.62% | −4,020 | identical |
| 40k_DTC | 1,392M → 1,349M | −3.10% | −136 | identical |
| 16plex_human | 1,767M → 1,713M | −3.06% | −2,132 | identical |
| 320k_GEMX | 2,740M → 2,678M | −2.26% | −7,306 | identical |

**Benchmarking (wall / peak).** Cost of the correction on the faithful path (before the `perf` cap), min-of-3:

| Dataset | wall OFF → ON | Δ wall | peak OFF → ON |
| --- | --- | ---: | --- |
| Flexv2_16k_Human | 78.4 → 84.7 s | +8.1% | 2.5 → 2.4 GB |
| 16k_mouse_Spleno | 110.6 → 118.3 s | +7.0% | 4.2 → 4.5 GB |
| 40k_DTC | 332.0 → 374.5 s | +12.8% | 8.6 → 9.7 GB |
| 16plex_human | 466.1 → 514.0 s | +10.3% | 6.7 → 6.6 GB |
| 320k_GEMX | 1253.8 → 1144.1 s | within I/O noise | 12.4 → 11.9 GB |

The `perf` cap (commit 2) is not reflected in that table — it cuts the resolver phase a further ~25% (see below), so the **shipped** ON cost is lower than the ON column. Peak is essentially unchanged (≤ ~1 GB).

**Profiling (40k_DTC, the `alevin-fry quant` phase, where the Hamming-1 pass runs).** The correction is fully parallel (~31 cores, same as OFF) and localized to the resolver phase:

- OFF: 29.6 s
- ON, faithful path (commit 1): 70.5 s
- ON, with the cap (commit 2, shipped): **52.6 s**

The resolver phase is ~9–17% of the whole pipeline (mapping dominates), which is why a doubled phase surfaces as only ~+13% total wall on the faithful path, and less with the cap.

## Tests

Ports Cell Ranger's own `test_correct_umis` cases and adds merge coverage: greater-count neighbour attracts reads and the low-support key is dropped; equal counts merge into the lexicographically larger UMI; no chaining (`a→b`, `b→c` decided on raw counts, both `b` and `c` survive); correction is per gene; 2-bit packing order equals lexicographic order over ACGT; an all-low-support cell yields an empty result that resolves without panicking.

Full `cargo test` green (58 lib incl. the 6 Cell Ranger vectors + the merge test, plus the atac/infer/multi_barcode/streaming integration suites); `cargo fmt --check` clean; clippy introduces no new warnings (the single `quant.rs` library warning pre-exists on `develop`).

## Credit

The core algorithm is by **@ygao61** (COMBINE-lab), from branch `umi_ham_edit_1` (`d92869f`); commit 1 carries her `Co-authored-by` trailer. This PR ports that work onto the current `develop`, adds the CLI gating + the USA / prefer-ambiguity guards + the logged tiny-cell override, and adds the output-identical UMI-length cap (commit 2).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f5cf1b862101`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.