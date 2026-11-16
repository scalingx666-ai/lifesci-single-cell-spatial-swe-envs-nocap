# Issue

**Title:** fix(io): --basename foo --paired produces foo_val_{1,2}.fq.gz

## Description

## Summary

Reported by @an-altosian (#244): in paired-end mode, \`--basename foo\` was producing \`foo_R1_val_1.fq.gz\` / \`foo_R2_val_2.fq.gz\` instead of the documented Perl v0.6.5+ form \`foo_val_1.fq.gz\` / \`foo_val_2.fq.gz\`. Trimmed read content was identical to Perl byte-for-byte; only the filenames differed — but that's enough to silently break every nf-core / Snakemake pipeline that constructs expected output paths as \`\${basename}_val_1.fq.gz\`.

## Root cause

\`io::paired_end_output_names\` and \`io::unpaired_output_names\` both built per-side stems as \`format!("{}_R1", b)\` / \`format!("{}_R2", b)\` even when \`--basename\` was supplied, then appended \`_val_{1,2}\` / \`_unpaired_{1,2}\` on top — producing the double-suffix shape \`foo_R1_val_1\`. The \`_val_{1,2}\` (or \`_unpaired_{1,2}\`) suffix already carries the pair-side distinction, so the \`_R{1,2}\` segment was redundant *and* divergent from Perl.

## Fix

When basename is supplied, use it as the stem directly for both sides:

\`\`\`rust
let (stem1, stem2) = match basename {
    Some(b) => (b.to_string(), b.to_string()),  // was: (format!("{}_R1", b), format!("{}_R2", b))
    None => (strip_fastq_extensions(input_r1), strip_fastq_extensions(input_r2)),
};
\`\`\`

Same fix in both functions.

## Historical note

The v0.6.5 CHANGELOG (19 Nov 2019) literally documents Perl having this exact bug and fixing it twice:

> *"In a \`--paired --basename BASE\` scenario, the output files will now be called \`BASE_val_1.fq.gz BASE_val_2.fq.gz\` as described in the documentation (we previously also added \`_R1\` and \`_R2\`). This had to be addressed twice (...) as the first approach was generating the Read 1 twice."*

The Rust port reintroduced the original v0.6.4 buggy form.

## Tests

Two new regression tests in \`io::tests\`:
- \`test_paired_end_output_names_with_basename\` — covers \`--output_dir\` on/off, gzip on/off
- \`test_unpaired_output_names_with_basename\` — covers the \`--retain_unpaired\` companion path

Total tests: 177 → 179.

## Test plan

- [x] \`cargo test --release\` — 179 passed
- [x] \`cargo fmt --all -- --check\` — clean
- [x] \`cargo clippy --all-targets --release -- -D warnings\` — clean
- [x] End-to-end smoke: \`trim_galore --paired --basename foo -o /tmp/smoke \\\\\\n  test_files/BS-seq_10K_R1.fastq.gz test_files/BS-seq_10K_R2.fastq.gz\` now produces \`foo_val_1.fq.gz\` and \`foo_val_2.fq.gz\` ✓
- [ ] CI validation matrix (md5 oracle path) — unaffected; this fix is filename-only

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `64ddb52078f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.