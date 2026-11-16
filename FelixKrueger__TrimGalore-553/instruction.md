# Issue

**Title:** fix(demux): reject duplicate barcodes in the sample sheet

## Description

## Problem

`demultiplex` opens one output writer per barcode and stores them in a `HashMap` keyed by barcode. If two sample-sheet lines share a barcode:

```
a	ACGTACGT
b	ACGTACGT
```

the second `insert` replaces the first writer, which is dropped unfinished. Sample `a` gets no output file, every read with that barcode goes to `b`, and the run exits 0. The output-collision pre-flight does not catch it because `<base>_a.fq.gz` and `<base>_b.fq.gz` are different paths.

Perl 0.6.11 has the same flaw in a different shape: `read_barcode_file` does `$barcodes{$barcode} = $sample`, so the last line wins and the first sample is silently dropped.

## Fix

`read_barcode_file` keeps a map of barcode → (line, sample) and bails on a repeat:

```
Barcode file bc.tsv line 3: barcode 'ACGTACGT' for sample 'b' was already given on line 1 for sample 'a' (each barcode must be unique)
```

The sheet is parsed in the output-collision pre-flight (`main.rs`), so the error comes before any trimming.

## Testing

- New unit test `demux::tests::test_read_barcode_file_rejects_duplicate_barcode`. It fails with the check disabled (the sheet parses `Ok`) and passes with it.
- `cargo test`: all suites pass (520 lib tests + integration tests).
- `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No output changes. Only sheets with a repeated barcode are affected, and those now error instead of producing output. The CI demux validation uses `test_files/demux_test_samplesheet.txt`, which has unique barcodes.

## Suggested CHANGELOG entry

- **A repeated barcode in the `--demux` sample sheet is now an error.** Previously the second line
  silently replaced the first, so the first sample got no output file and its reads went to the
  other sample with exit 0. The error names both line numbers and both sample names.

Part of #546 (finding 4 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9c6b4000154`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.