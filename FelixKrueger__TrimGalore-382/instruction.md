# Issue

**Title:** fix(io): strip .bgz/.bgzf so output and report share a stem

## Description

.

## The problem

Since #374 a gzipped input named `.fq.bgz` is read correctly, but its trimmed output and its trimming report stopped agreeing on the sample name:

```
$ trim_galore -o out_bgz --dont_gzip sample.fastq.bgz
$ ls out_bgz/
sample.fastq_trimmed.fq
sample.fastq.bgz_trimming_report.json
sample.fastq.bgz_trimming_report.txt
```

The same bytes under a `.fastq.gz` name give `sample_trimmed.fq` next to `sample.fastq.gz_trimming_report.txt`, both resolving to the sample `sample`. MultiQC takes the sample name from the report filename, so on the `.bgz` input the trimmed file and its report can land under different samples.

`io::strip_fastq_extensions` walked an ordered list holding only the `.gz` forms, so `sample.fastq.bgz` matched none of them and reached the `Path::file_stem` fallback, which strips the final component only and leaves `sample.fastq`. The report name is built from the full input filename, which is why it was unaffected and why the two diverged.

## The fix

Strip a gzip-family suffix (`.gz`, `.bgz`, `.bgzf`) and then the FASTQ extension, rather than enumerating the combined suffixes:

```rust
let stem = [".gz", ".bgz", ".bgzf"]
    .iter()
    .find_map(|ext| name.strip_suffix(ext))
    .unwrap_or(&name);

for ext in [".fastq", ".fq"] {
    if let Some(base) = stem.strip_suffix(ext) {
        return base.to_string();
    }
}
```

The two groups are disjoint (`.bgz` does not end in `.gz`), and splitting them means a new compression name costs one list entry instead of doubling the cases.

On the two open questions in the issue:

* **`.bgzf`** is included. It is the other name bgzip output is given in the wild, and on this shape it is one array element.
* **A bare `.bgz`/`.bgzf`** with no inner `.fastq`/`.fq` already worked, via the `file_stem` fallback, and is now pinned by a test so the rewrite cannot lose it.

## Scope and risk

Output *filenames* only. Nothing in `test_files/` and nothing in the `validation` matrix is named `.bgz`, so the Perl-0.6.11 byte-identity comparison does not move. `.bam` inputs, bare `.gz`, and unrelated extensions keep the stems they had, pinned by a second unit test.

The related limitation the CHANGELOG records separately, that output compression still mirrors the input filename so a `.bgz` input produces plain `.fq` output, is **not** touched here. It changes behaviour on every run and deserves its own discussion.

## Tests

Written first, and each watched to fail for the right reason before the fix went in:

* `io::tests::test_strip_fastq_extensions_bgz` covers `.fastq.bgz`, `.fq.bgz`, `.fastq.bgzf`, `.fq.bgzf`, `sample_R1.fq.bgz` and the bare forms. Fails on `dev` with `left: "sample.fastq", right: "sample"`.
* `io::tests::test_strip_fastq_extensions_leaves_other_names_alone` pins `.bam`, bare `.gz`, `.txt.gz` and a bare stem.
* `bgz_output_and_report_agree_on_the_stem` runs the issue's reproduction through the binary under three names, `.fastq.bgz`, `.fq.bgz`, and a `.fastq.gz` control, asserting the same output/report relationship for each. Against unfixed code it reports the issue's exact symptom: `expected output .../sample_trimmed.fq, found ["sample.fastq_trimmed.fq", "sample.fastq.bgz", "sample.fastq.bgz_trimming_report.json", "sample.fastq.bgz_trimming_report.txt"]`.

The existing `.bgz` integration tests in that file move to the tidy stems (`pair_R1_val_1` rather than `pair_R1.fq_val_1`); their module docs recorded the old names as a known wart and now point at the new test instead.

Local: `cargo test` all green (383 lib + integration suites), `cargo fmt --all -- --check` clean, `cargo clippy --all-targets --release -- -D warnings` clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ca9596269ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.