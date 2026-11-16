# Issue

**Title:** perf(quant): resolve each cell over its own features, not the whole axis

## Description

## Summary

For every cell outside the tiny-cell fast path, `quant` allocated, zeroed and scanned vectors over the whole feature axis, even though a cell only touches the features its equivalence classes name. That axis is the genes, or under `quant-probe` (#204) the probes: 53,519 of them for the human Flex v2 probe set, against 18,132 genes. The dense work is why `quant-probe` cost 18–34% more than `quant` on Flex.

`SparseCellCounts` (`src/em.rs`) is a per-worker buffer whose per-cell passes walk only the cell's support:
- **What it replaces:** the unique-count and EM steps of `em_optimize`, the trivial resolver's dense vector, and USA-mode `extract_counts`.
- **Output:** the cell's nonzero entries, in increasing feature order.
- **EM equivalence:** the EM keeps `em_optimize`'s steps and order within the support. A feature outside the support appears in no class and is zero after the first iteration either way, so results are bit-identical for the uniform and informative initializations.
- **Unchanged:** the USA-mode and long-read EMs keep their dense vectors, and bootstrapping rebuilds a dense vector.

## Results

**Output is unchanged.** On 34 configurations, matrices (gene and probe), `featureDump.txt` and `quant.json` are identical to `develop` without this change (at 288649b).
- **Flex:** `quant` and `quant-probe` under cr-like, cr-like-em, parsimony, parsimony-em and trivial, ±`--probe-mtx`; `--umi-edit-dist 1`; `--small-thresh 0`; `-d`; `--dump-molecules`; `-b 2 --summary-stat`.
- **PBMC1k:** both subcommands with a 2-column map, plus USA mode.
- New unit tests check `SparseCellCounts` bit for bit against `em_optimize`, the dense extraction scan and `extract_counts`, reusing one buffer across cells.

**Speed** on a 384-plex Flex v2 library (262k cells), 16 threads, median of 5, with the two builds alternating:

| strategy | `quant-probe` before → after | `quant` before → after |
|---|---|---|
| cr-like | 1.94 → 1.58 s (−19%) | 1.59 → 1.49 s (−6%) |
| cr-like-em | 2.53 → 1.62 s (−36%) | 1.91 → 1.56 s (−18%) |
| parsimony | 2.19 → 1.83 s (−16%) | 1.86 → 1.77 s (−5%) |
| parsimony-em | 2.69 → 1.87 s (−30%) | 2.11 → 1.80 s (−15%) |
| trivial | 1.83 → 1.50 s (−18%) | 1.52 → 1.43 s (−6%) |
| cr-like `--umi-edit-dist 1` | 2.11 → 1.62 s (−23%) | 1.70 → 1.55 s (−9%) |
| cr-like-em `--probe-mtx` | 2.86 → 1.95 s (−32%) | — |

- `quant-probe` now costs 3–6% more than `quant`, down from 18–34%.
- Standard 10x 3' data is unaffected (PBMC1k USA: 0.10 s either way), because nearly every cell there takes the fast path.
- Peak RSS moves by −5% to +7% between cases, with no consistent direction (one run per build per case, about 0.5 GB). The per-worker buffers are three axis-length vectors.

## API

`pugutils::get_num_molecules_trivial_discard_all_ambig` now writes into a `&mut SparseCellCounts` and returns only the multi-gene fraction. This is noted in the CHANGELOG, and is fine for a pre-1.0 minor release. Neither simpleaf nor piscem-infer links alevin-fry as a library.

## Testing

All 153 tests pass; clippy and fmt are clean.

**Independent adversarial review: no output change found.** The reviewer checked the sparse EM line by line against `em_optimize`/`em_update`, and checked buffer state across cells and the routing of every resolver arm. Two further checks were run:
- **Randomized buffer test:** 3,000 generated cells on axes from 7 to 53,519 features, with one buffer reused throughout, under both initializations. Every result was bit-identical, with EM iteration counts from 2 up to `MAX_ITER`.
- **40 more end-to-end comparisons, all identical.** They used `--small-thresh 0`, so every cell takes the sparse path; USA `--sa-model prefer-ambig`; `-b 3` and `--init-uniform`; `--large-graph-thresh` 0/1; `-d --dump-molecules`; and Flex parsimony-em with 22k alternative-resolution cells.

Following the review, `unique_counts` and `em` reset the buffer themselves, as the other fillers do, and the EM's scratch vector is sized only when the EM runs. A recheck of 9 configurations was identical, with unchanged timing.

The CHANGELOG gains a Performance entry, and the `quant-probe` cost bullet from #204 is updated to the new numbers.

Intended for 0.19.0.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01TtmwfkBMvwsCxdQrf4RTPN

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `288649ba8c11`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.