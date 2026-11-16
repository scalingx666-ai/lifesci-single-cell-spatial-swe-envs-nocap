# Issue

**Title:** fix(demux): reject sample names that are empty or contain a path separator

## Description

## Problem

The demux sample name from the sample sheet is joined straight into the output file name (`<base>_<sample>.fq.gz`), and `FastqWriter::create` creates any missing parent directories. A sheet line

```
x/../../escaped	ACGTACGT
```

with `-o d5/out` wrote `d5/escaped.fq.gz`, outside the output directory, with exit 0. An empty sample name (line starting with a tab) produced `<base>_.fq.gz`.

Perl 0.6.11 does no validation either: `read_barcode_file` just splits on tab, and `open_barcode_filehandles` opens `"${output_dir}${base}_$sample.fq"` directly (or through `| gzip -c - > ...` in a shell when gzipping). There a `/` in the name only works if the intermediate directories already exist, because Perl does not create them; the Rust port does, so the escape always succeeds.

## Fix

`read_barcode_file` bails when a sample name is empty or contains `/` or `\`:

```
Barcode file bc.tsv line 2: sample name must be non-empty and must not contain '/' or '\'. Got: 'x/../../escaped'
```

The sheet is parsed in the output-collision pre-flight (`main.rs`), so the error comes before any trimming. Names such as `..` with no separator stay allowed; they only produce `<base>_...fq.gz` inside the output directory.

## Testing

- New unit test `demux::tests::test_read_barcode_file_rejects_path_like_sample_names` covers `x/../../escaped`, `a\b` and the empty name. It fails with the check disabled (the sheet parses `Ok`) and passes with it.
- `cargo test`: all suites pass (846 tests).
- `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No output changes for valid sheets. The CI demux validation sheet (`sample1`, `sample2`, `sample3`) is unaffected.

## Suggested CHANGELOG entry

- **`--demux` sample names can no longer write outside the output directory.** A sample name is
  part of the output file name, so `x/../../escaped` used to write two levels up. Sample names that
  are empty or contain `/` or `\` are now rejected with the offending line.

Part of #546 (finding 6 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `93acb7f651a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.