# Issue

**Title:** feat(quant): --dump-molecules writes a per-molecule Parquet table

## Description

.

## What

`alevin-fry quant --dump-molecules` writes `alevin/molecules.parquet`: one row per molecule produced by UMI resolution, before molecules are summed into `quants_mat.mtx` (similar in spirit to Cell Ranger's `molecule_info.h5`). It works with every resolution strategy, in USA mode, and for multi-sample (Flex) input.

| column | meaning |
|---|---|
| `cell_barcode` | corrected cell barcode (dictionary) |
| `sample` | sample name, multi-sample input only (dictionary; null if the manifest has no name) |
| `rep_umi` | **representative** UMI (see below) |
| `n_umis` | distinct observed UMIs collapsed into this molecule |
| `feature` | matrix column the molecule was counted in; null if gene-ambiguous (dictionary) |
| `candidate_features` | list of compatible features when `feature` is null |
| `reads` | reads supporting the assignment |
| `status` | `assigned` / `multi_gene` / `low_support` (dictionary) |

The column is called `rep_umi` because a row is not always one observed UMI:
- **cr-like / cr-like-em:** the UMI itself, or with `--umi-edit-dist 1` the corrected UMI that its Hamming-1 neighbours were merged into.
- **parsimony\*:** the root of the covering arborescence; all covered UMIs are collapsed into the row.
- **trivial:** the UMI itself.

`low_support` rows (from `cr-like --umi-edit-dist 1`) are one per UMI that the filter drops *entirely* (a tie or chimera). The losing keys of a UMI that keeps a winner are not rows, just as plain cr-like does not emit a UMI's losing genes.

For the non-EM strategies, counting `assigned` rows per (cell, feature) reproduces `quants_mat.mtx` exactly. Cells on the tiny-cell fast path are recorded with that path's cr-like semantics, which is how they are counted.

## How

- **Recording:** each resolver records molecules at the point where it commits them. That covers both cr-like resolvers, the Hamming-1 correction, trivial, PUG covers, the large-component fallback and the tiny-cell fast path. The parameter is an `Option`, so default runs do no extra work (see the note on layout below).
- **Shared column rule:** the USA-mode "which column does this label set count in" rule is moved from `extract_counts` into `utils::usa_label_column`, so the matrix and the table share one rule. Behaviour is unchanged; see validation.
- **Parallel writing:** each quant worker fills its own 128Ki-row row group, then encodes and compresses it without holding a lock, via parquet's `ArrowRowGroupWriterFactory`. Only appending the finished column chunks to the file is serialized.
- **Dependencies:** `parquet` with only `arrow` + `lz4`, plus `arrow-array` and `arrow-schema`, all at 60.0. LZ4 is `lz4_flex`, already used by libradicl for collated chunks. No C code enters the default build.

## Choosing the format

Writers were benchmarked on rows generated from the real PBMC 5k matrix (24.5M molecules):

| format | bytes/row | write, 32 threads, 98M rows | load, 24.5M rows (polars / pyarrow) |
|---|---|---|---|
| **Parquet, one file, parallel row groups** (chosen) | 9.0 (snappy) / 6.9 (zstd) | 112–128 M rows/s | 0.03 s / 0.29 s |
| Parquet, one file per worker | same | 172 M rows/s | 0.03 s / 0.13 s |
| Arrow IPC stream (lz4) | 30.0 | 77 M rows/s | 0.82 s / 0.12 s |
| gzip TSV (level 1) | 15.9 | 104 M rows/s | 1.7 s / 15.9 s (pandas) |

Single-file Parquet keeps one output file at near-sharded write speed.

**Codec: LZ4 (Parquet LZ4_RAW).** Snappy vs LZ4 on the real tables (re-collated PBMC 5k, 32 threads):

| | quant wall, no table | Snappy | LZ4 | file (Snappy / LZ4) |
|---|---|---|---|---|
| standard, 33M molecules | 2.24 s | 2.47 s | **2.42 s** | 458 / 457 MB |
| USA, 70M molecules | 5.05 s | 5.54 s | **5.45 s** | 758 / 832 MB |

Load times are the same for both (pyarrow 0.21–0.23 s, polars 0.11–0.23 s, DuckDB query 0.01–0.02 s). LZ4 writes a little faster, matches collate's codec and adds no dependency. Snappy is ~10% smaller in USA mode and readable by older tools (LZ4_RAW needs roughly pyarrow ≥ 10).

## Validation

Real data: PBMC 5k 10x 3' v3, both a standard and a splici (USA) reference, plus a Human Kidney 4k GEM-X Flex multi-sample run; 32 threads. For each configuration:
1. The table's `assigned` rows reproduce the matrix: exactly for non-EM strategies, never exceeding it for EM strategies.
2. The matrix is identical with and without `--dump-molecules`.
3. The matrix of this branch without the flag is identical to `develop`.

All three passed for all 15 configurations:
- **standard:** cr-like, cr-like `--umi-edit-dist 1`, cr-like-em, trivial, parsimony, parsimony-gene, parsimony-em, parsimony-gene-em, parsimony `--small-thresh 0`
- **USA:** cr-like, cr-like `--sa-model prefer-ambig`, cr-like-em, parsimony
- **Flex:** cr-like, cr-like `--umi-edit-dist 1`

New unit tests cover the cr-like correction and resolver recording, USA/standard label assignment, and a Parquet write/read round trip (two row groups, dictionary columns, list column, null sample). clippy and fmt are clean, and the full suite passes in debug and release.

## Costs

Measured on PBMC 5k re-collated by current `develop` (per-chunk LZ4 with a chunk index, so quant reads in parallel), 32 threads, mean of 3:
- **Wall time with the flag:** +8% (2.24 → 2.42 s standard; 5.05 → 5.45 s USA). The added time is the workers encoding 33M–70M rows. It was hidden in the first version of this description, which timed legacy whole-file `.sz` collations where quant's single-threaded reader dominated.
- **Memory with the flag:** about +1.1 GB peak RSS at 32 threads (1.76 → 2.88 GB standard). This is mostly per-worker row-group buffers kept by mimalloc; bounding it independently of thread count would mean dedicated encoder threads, which could be a follow-up.
- **File size:** 457 MB standard, 832 MB USA.
- **Binary size:** 6.5 MB → 11.3 MB.
- **Without the flag:** output unchanged, and no speed difference: `develop` 2.31 s vs this branch 2.26 s (standard), 5.23 vs 5.11 s (USA). An earlier ~1.5% gap on legacy `.sz` collations came from the serial Snappy stream reader and code layout. It persisted under fat LTO and `codegen-units = 1` too, and does not occur on current collations, so no build-profile change is included.

## Noted, not changed here

The Flex fixture used for validation was collated by alevin-fry 0.11.2, before collation recorded sample ordinals (fixed in 0.15.0). On it, quant cannot name some cells' samples, and the table writes a null `sample` for them. Quant-side handling of such collations is in a separate PR.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RRoQ4mpDcUwtsSz5aedxtM

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edfd1aae5426`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.