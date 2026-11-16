# Issue

**Title:** fix(genemap): accept gzip-compressed GTF/GFF for --geneMap

## Description

.

`--geneMap Homo_sapiens.GRCh38.115.gtf.gz` failed with `stream did not contain valid UTF-8`, and only after mapping, EM and `quant.sf` had all finished. Gzip is how Ensembl and GENCODE ship annotations, so this is the invocation people reach for first, and it cost a full run to discover.

## Root cause

[`read_transcript_gene_map`](https://github.com/COMBINE-lab/salmon/blob/develop/crates/salmon-core/src/genemap.rs#L16) in `crates/salmon-core/src/genemap.rs` opened the path as plain text:

```rust
let reader = io::BufReader::new(std::fs::File::open(path)?);
for line in reader.lines() {
    let line = line?;          // ← BufRead::lines() validates UTF-8; gzip magic fails here
```

It surfaces at the end of the run because gene-level aggregation is the last step: `write_gene_level` is called from `main.rs:1612` after `quant.sf` is written, and opens the gene map as its first action.

This is **not a regression.** I checked the `cpp` branch before writing any code, because "it used to work" would have changed the fix. `generateGeneLevelEstimates` in `src/util/SalmonUtils.cpp` dispatches on the same extension set (`.gtf/.gff/.gff3` and uppercase), so `.gtf.gz` fell through to the two-column branch, where `while (ifile >> transcript >> gene)` consumed compressed bytes as tokens without complaint. C++ built a garbage map silently. 2.x already turned that into a loud failure; this PR makes the format work instead.

## The part that is easy to get wrong

Adding decompression alone would have been a bug. `is_gtf` came from the *last* extension:

```rust
let is_gtf = matches!(ext.as_str(), "gtf" | "gff" | "gff3");
```

For `annotation.gtf.gz` that is `gz`, so the decompressed GTF would have been handed to the TSV branch, whose first two whitespace-separated fields on a GTF line are the sequence name and the source. Measured against the reader as it stands, by giving it a GTF named `annotation.txt`:

```
parsed_as_tsv entries=1 content={"1": "havana"}
```

One bogus entry. Non-empty, so the `map.is_empty()` guard does not fire; no transcript matches; `quant.genes.sf` comes out empty and the run exits 0. That is exactly the silent failure in #1075 — so the naive fix would have traded a loud bug for a quiet one. `has_gtf_extension` strips a trailing `.gz` before deciding, and `reads_gzipped_gtf` pins it: the assertion is on the parsed pairs, so a TSV misparse fails the test.

## What changed

- **Detection by magic bytes, not by name.** `BufRead::fill_buf` peeks the leading `1f 8b` without consuming, so a compressed annotation that kept a bare `.gtf` name also works.
- **`MultiGzDecoder`, not `GzDecoder`.** Concatenated gzip members are legal; a single-member decoder stops at the first member's end and returns a *partial* map with no error. Covered by `reads_multi_member_gzip`.
- **`.gz`-aware GTF/TSV detection**, per above.
- **Errors name the file and hint at the cause.** `File::open`, the sniff and the line loop are all annotated:

  ```
  reading gene map /path/Homo_sapiens.GRCh38.115.gtf.bz2: stream did not contain
  valid UTF-8 (expected plain text or gzip; annotations compressed with anything
  else, such as bzip2 or zstd, must be decompressed first)
  ```

  The underlying message is preserved rather than replaced, so a truncated gzip still reports as a gzip failure. The caller's `.with_context("reading gene map {path}")` in salmon-cli is dropped, since it would now print the path twice.
- **Docs**: `--geneMap` help text, the CLI reference table, and the quick-start bullet.

## Before / after

| Input | Before | After |
|---|---|---|
| `annotation.gtf` | 2 pairs | 2 pairs |
| `t2g.tsv` | 2 pairs | 2 pairs |
| `annotation.gtf.gz` | `Error: stream did not contain valid UTF-8`, after the full run | 2 pairs |
| `t2g.tsv.gz` | same error | 2 pairs |
| gzip content named `.gtf` | same error | 2 pairs |
| multi-member `.gtf.gz` | same error | 2 pairs (not truncated) |
| `.gtf.bz2` | `stream did not contain valid UTF-8` | same, plus file name and what was expected |
| missing file | bare errno | `reading gene map <path>: No such file or directory` |

`salmon-core` goes from 20 to 30 tests.

## Commits

Four, each self-contained, each with its test in the same commit:

1. `test(genemap): cover plain, gzip and TSV gene-map inputs` — the gzip case is `#[ignore]`d with a pointer to #1074 so the commit is green and the series bisectable. I checked it fails for the documented reason, not incidentally: `called Result::unwrap() on an Err value: Error { kind: InvalidData, message: "stream did not contain valid UTF-8" }`.
2. `feat(genemap): detect gzip by magic bytes and decompress transparently` — removes the `#[ignore]` in the same commit.
3. `fix(genemap): surface the file path and a hint in reader errors`
4. `docs: state that --geneMap accepts gzip-compressed GTF/GFF`

Verified per commit, not just at the tip — `cargo fmt --all --check`, `cargo clippy -p salmon-core -p salmon-cli --all-targets` and `cargo test` on each of the four:

```
4ca1355f test(genemap): cover plain, gzip and TSV  | fmt=OK clippy_errors=0 test_failures=0
abc46086 feat(genemap): detect gzip by magic bytes | fmt=OK clippy_errors=0 test_failures=0
63b26d71 fix(genemap): surface the file path       | fmt=OK clippy_errors=0 test_failures=0
648f6b70 docs: state that --geneMap accepts gzip   | fmt=OK clippy_errors=0 test_failures=0
```

`cargo test --workspace` is green at the tip. The pre-existing clippy warnings in salmon-model, salmon-align and salmon-map are untouched and also present on `develop`.

## Dependency

`flate2` moves into `salmon-core`'s `[dependencies]`. It is already a workspace dependency used by `salmon-quant`, `salmon-align` and `salmon-model`, so the dependency tree does not change — `salmon-core` only opts in.

## Deliberately not addressed

- **`--geneMap` is still not validated before mapping starts.** A bad path or an unreadable annotation still costs the whole run before it is reported. Worth fixing, but it is a change to the CLI's startup ordering rather than to the reader, so I left it out; happy to do it separately if you want it.
- **Other compression formats** (bzip2, zstd). The error now names them as things to decompress rather than supporting them; adding codecs seemed like scope creep for a bug report about the format Ensembl actually ships.
- **The empty-`quant.genes.sf` problem** is #1075 and is independent — different cause, different fix, no overlap with this branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01e37dabc79c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.