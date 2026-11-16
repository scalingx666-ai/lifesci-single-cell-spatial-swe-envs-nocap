# Issue

**Title:** fix: make the filtered permit list order-independent

## Description

## The bug

`generate-permit-list` in any of its filtered modes (`-k`, `--expect-cells`, `--force-cells`) does not produce the same output twice on the same input.

`permit_list_from_threshold` builds `valid_bc` by iterating `hist`:

```rust
let valid_bc: Vec<u64> = hist
    .iter()
    .filter_map(|(k, v)| if v >= &min_freq { Some(*k) } else { None })
    .collect();
```

`hist` is a `HashMap` obtained by draining a `DashMap` that the parsing threads filled concurrently, so its iteration order reflects the order those threads happened to insert. That order is then load-bearing: `generate_permitlist_map` walks `valid_bc` and does `entry(neighbour).or_insert(bc)`, so a barcode one edit away from two different retained barcodes is corrected to whichever of them comes first. Change the thread interleaving and some barcodes correct elsewhere, moving UMI counts between cells.

## Reproduction

Toy dataset from the `sample_run` CI job. Three runs of `generate-permit-list -k` + `collate` + `quant -r cr-like`, same binary, same input, comparing per-barcode count vectors (re-keying each nonzero of `quants_mat.mtx` by its barcode, so row ordering is not what is being compared):

| comparison | cells with differing counts |
|---|---|
| run 1 vs run 2 (before) | 14 / 1,151 |
| run 2 vs run 3 (before) | 10 / 1,151 |
| run 1 vs run 2 (after) | **0 / 1,151** |
| run 1 vs run 3 (after) | **0 / 1,151** |

Counts move in pairs, as expected from a correction target changing: for one barcode column 8099 goes from 1 to absent while a neighbouring barcode gains it.

The `--unfiltered-pl` path does not call this function and was already stable across three runs.

## The fix

One `sort_unstable()` on `valid_bc`, with a comment explaining what depends on the order.

Which barcode *should* win an ambiguous neighbour is a separate question. Lowest packed barcode is arbitrary; resolving by observed read frequency would be more defensible, and `hist` is right there if the maintainers want that instead. This change only removes the dependence on thread scheduling, and deliberately does not relitigate the tie-break.

## Checks

- `cargo test --workspace`: 24 passed, 1 ignored, 0 failed
- `cargo clippy --workspace --all-targets`: clean
- `cargo fmt --check`: clean

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ad7e74b3c34`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.