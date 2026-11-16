# Issue

**Title:** fix(io): match FASTQ extensions case-insensitively

## Description

. `SAMPLE.FASTQ.GZ` kept an inner `.FASTQ` in its output stem while the report used the full filename, so the two disagreed about the sample name. Extension matching (`.fastq`/`.fq`, `.gz`/`.bgz`/`.bgzf`) now folds ASCII case, so uppercase input behaves exactly like lowercase: `SAMPLE_trimmed.fq.gz` beside `SAMPLE.FASTQ.GZ_trimming_report.txt`.

Behaviour changes for uppercase-named input, all listed in the CHANGELOG: output is renamed and now gzip-compressed; multi-input runs whose extensions differ in spelling but whose stems now agree are refused before any file is written; `--clump_only` report labels shift; the specialty modes rename the same way. Perl v0.6.11 had no naming mismatch here (its fallback appended to the full name), so pinning the old output would have preserved a rewrite-only defect — the reasoning is recorded on the issue.

<details>
<summary>Detail (AI-assisted; bin freely)</summary>

Two functions fold, deliberately together: `strip_fastq_extensions` (output stem) and `is_gzipped` (output compression). Folding only the stem would name uppercase output like the gzipped convention while writing it plain. On compression this knowingly departs from v0.6.11 (whose test was also case-sensitive); on naming, parity was already lost to the `file_stem()` fallback.

The suffix strip is byte-wise — the naive `&str` slice panics mid-character on multi-byte filenames that work end-to-end today. Caught at plan review, along with two more Criticals: the first draft's collision test asserted a refusal that already happens via the case-folded report keys (so it could never fail), and three `is_gzipped` call sites in `clump_only.rs` were missing from the caller enumeration.

**Verification.** 540 tests (10 new), fmt + clippy clean. Both negative controls discriminate: reverting either half alone fails that half's tests. The V8 report assertion targets the `Input:` line specifically, because the `Output:` line contains "gzip level N" unconditionally and a whole-report substring match cannot pin the input label. Pure case-variant pairs are already refused today and are deliberately not used as test fixtures.

No fixture in `test_files/` and no CI invocation uses an uppercase extension, so the Perl byte-identity matrix is untouched.

**Artefacts** in `plans/08072026_uppercase-fastq-extensions/`: plan (v2), two plan reviews (3 Criticals, all pre-implementation), two code reviews (0 Critical / 0 High), coverage audit (one gap, closed).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `533582aa037f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.