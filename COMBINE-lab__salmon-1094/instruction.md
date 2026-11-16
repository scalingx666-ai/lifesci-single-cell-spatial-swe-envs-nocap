# Issue

**Title:** perf(eqclass,infer): stop copying the largest structures needlessly

## Description

Part of #1092 (performance / memory audit). Two independent allocation fixes on the equivalence-class path, no behavioural change.

### `EquivalenceClassBuilder::finish` cloned a map it already owns

`finish` takes `self` by value, so the concurrent map is dropped either way. It nonetheless cloned every key and value out of it, and those clones are deep: `TranscriptGroup` owns two `Vec<u32>`, and `TGValue` owns the `Vec<u128>` fixed-point accumulator, which is still live at that point.

The effect was two full copies of the largest structure in the run held simultaneously, plus a heap allocation and a memcpy per class per vector. `DashMap` implements `IntoIterator`, so the entries can simply be moved. .

### `PackedEqClasses::from_collapsed` did not reserve

`labels`, `combined` and `weights` grew from empty to tens of millions of elements: a reallocation and full copy at every doubling, plus a transient peak of roughly 1.5x the final size while both buffers are live. `starts` was already reserved correctly, which shows the intent; the other three were missed. The exact total is one cheap pass over the class list (it only reads `Vec::len`). .

### CSR offsets could truncate silently

While in `from_collapsed`: the offsets are `u32` and `starts.push(labels.len() as u32)` wrapped silently past `u32::MAX` incidences. After that `class()` hands the optimizer slices belonging to *other* classes — wrong abundances, no panic, no warning, no diagnostic of any kind.

4.29 billion incidences is ~17 GB of `labels`, so this is not a small-index concern; it is reachable on a heavily multi-mapping library against a large decoy-aware index, which is exactly where nobody would think to suspect arithmetic. This adds an assertion so the limit fails loudly instead of producing plausible nonsense. Widening `starts` to `u64` would remove the ceiling rather than report it, and is a reasonable follow-up if you would prefer that. .

### Verification

- `cargo test --workspace` passes; `cargo clippy --workspace --all-targets` adds no warnings; `cargo fmt` clean.
- Built against `develop` and compared to a `develop` baseline binary on `sample_data`: `quant.sf` byte-identical for plain, `--seqBias --gcBias --posBias`, and `--softclip` runs; `meta_info.json` (modulo timing) and `lib_format_counts.json` identical.

Caveat worth stating: `sample_data` has 15 transcripts, so the parity check confirms the code paths agree, not that the memory behaviour holds at transcriptome scale. The memory claims here are structural (fewer copies of the same data), not measured. I have not benchmarked peak RSS on a human-scale index.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d452cd977c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.