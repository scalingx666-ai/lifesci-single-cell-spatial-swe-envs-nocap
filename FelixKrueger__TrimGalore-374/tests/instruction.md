# Issue

**Title:** fix(io): read gzipped input whose filename does not end in .gz

## Description

## The bug

`detect_input_format` classifies input from file **content** (that is the whole point: `bgzip x.fq` and a `samtools import` BAM are indistinguishable at the gzip-header layer, so the discriminator is the decompressed payload). But that verdict was then thrown away and re-derived from the **filename** in three separate places:

- `FastqReader::open` (`src/fastq.rs:253`)
- `FastqReader::open_threaded`, via `open_direct` (`src/fastq.rs:341`)
- `FastqReader::sanity_check`, which calls `open`

So a `bgzip`-produced `.fq.bgz` was correctly detected as `FastqGz` and then read as raw text. Reproduced on `dev`:

```
$ gzip -c reads.fq > reads.fq.bgz
$ trim_galore reads.fq.bgz
Trim Galore v2.3.0
==================================================

Error: stream did not contain valid UTF-8
```

`sanity_check` runs before everything else in `main()`, so that is where it died: before adapter detection, before any output directory was created.

## The fix

Pass the detected format down instead of re-deriving it.

- New `FastqReader::open_with`, `::open_threaded_with`, `::sanity_check_with` take the gzip verdict from the caller.
- `format::open_sync_reader` / `open_threaded_reader` and `main::sanity_check_any` already call `detect_input_format`; they now hand its answer over. Public signatures are unchanged, so no call site outside these files moves.
- The filename heuristic stays for callers that have not run detection, but as one named function (`is_gz_filename`) rather than three inline copies.

Also deletes `main.rs`'s private duplicates of `format::open_sync_reader` and `format::open_threaded_reader` (`src/main.rs:47` and `:64`). They were behaviourally identical to the `format::` versions (not *byte*-identical: `open_sync_reader` differs by a trailing comma, because `crate::fastq::` pushes the match arm past 100 columns and rustfmt brace-wraps it). This fix would otherwise have had to be applied twice; that duplication is arguably how the bug survived.

## Tests

Six new regression tests, covering the sync reader, the threaded reader (the verdict has to cross a thread boundary), `sanity_check`, and both `format::` factories. One asserts the mirror-image case: a caller passing `false` for a `.gz`-named plain file must win over the filename.

One test deliberately asserts `FastqReader::sanity_check(&p).is_err()` on a `.bgz` file: the filename-based entry point is *supposed* to still get it wrong, which is why callers holding a content-detected verdict must not use it.

Verified end to end: `.fq.bgz` now trims at `--cores 1` and `--cores 4`, producing records byte-identical to the same data named `.fq.gz`.

Full suite green (375 unit + integration), `cargo fmt --check` and `cargo clippy --all-targets --release -- -D warnings` clean.

## Known limitation, not fixed here

Output compression still mirrors the input **filename** (`io::is_gzipped`), so a `.bgz` input produces plain `.fq` output. Moving that decision to the detected format would change behaviour for every run, including a plain file misnamed `.gz`, so it seemed to belong in its own change rather than riding along with a read-path fix. Noted in the CHANGELOG.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

---

## Update after review

@FelixKrueger found that the first version stopped one layer short, and that on `--paired` this was a regression rather than a missed case: fixing `sanity_check_any` let the run reach `FastqWriter::create`, which truncates, before failing on the first read. Base `dev` failed earlier and left existing output intact.

Fixed in `16d47ca` + `a293a1b`:

- **`is_gz_filename` is now `sniff_gzip`**, a three-byte gzip-magic check. The default is correct rather than the verdict being threaded to eight more call sites, which closes `--paired --cores 1`, `--passthrough` and `--clump_only` in one edit. No BAM logic, so `fastq` gains no dependency on `format`; deliberately not `detect_input_format`, which bails on empty input that `demux` legitimately reads back.
- **Dropped the test that pinned the bug as a contract.** It asserted little and would have read as a regression to whoever made `open` correct.
- **`io.rs` doc corrected** — it claimed to be the same heuristic the reader uses, which this PR makes false.
- **Integration tests added**, chosen by dispatch path: SE, PE `--cores 1`, PE `--cores 2`, `--clump_only`, serial-vs-parallel agreement, and the misnamed-plain case.
- **CHANGELOG records both directions.** A plain FASTQ misnamed `.fastq.gz` previously failed with `invalid gzip header` and now reads.

468 tests pass; `fmt` and `clippy -D warnings` clean; byte-identity on ordinary inputs re-confirmed against a pre-change build.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7201f03e95aa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.