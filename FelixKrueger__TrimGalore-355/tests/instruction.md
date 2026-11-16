# Issue

**Title:** feat(clump-only): add --clump_only lossless reorder-only mode

## Description

(requested by @wkgardner).

## Summary

New run-and-exit specialty mode that reorders FASTQ records by canonical 16-mer minimizer for gzip-friendly compression **without any trimming, filtering, or adapter detection**. Output records are byte-identical to input records (header + sequence + quality); only file-level order changes. Same clumping win \`--clumpify\` delivers as a compression stage inside the trim pipeline, but as a standalone lossless mode for archival / recompression pipelines that need the size win with record-level fidelity.

## Contract

**Preserved byte-identically:** read ID, sequence, quality string.

**Normalized codebase-wide** (inherited from \`FastqReader\`/\`FastqWriter\`, not \`--clump_only\`-specific):
- Plus-line (line 3) → bare \`+\` on output
- CRLF line endings → LF on output

Documented explicitly in the mode's \`--help\` text, docs page, and PLAN.md §Contract-scope note. Regression-guard tests for both normalizations landed.

## Composability

**Composes with:** \`--paired\`, \`--compression\`, \`--memory\`, \`--cores\`, \`--fastqc\`, \`--dont_gzip\`, \`--basename\`, \`--no_report_file\`.

**Rejected at CLI validation:** all trim/filter/clip/adapter flags, other specialty modes, \`--output-format ubam\`, \`--passthrough\`, \`--retain_unpaired\`. \`-q\` / \`--stringency\` / \`-e\` silently ignored (clap defaults on non-\`Option\` types; matches \`--hardtrim5\` convention).

## Outputs

- SE: \`*_clumped.fq(.gz)\`
- PE: \`*_clumped_{1,2}.fq(.gz)\`
- Report: \`*_clumping_report.txt\` (text-only, deliberately outside the \`*_trimming_report.*\` glob so downstream nf-core/MultiQC scanners don't mis-classify an empty-of-trim-stats file).

v1 is FASTQ in / FASTQ out only. uBAM in/out is a natural v2 follow-up; uBAM input is rejected at \`format::detect_input_format\` dispatch time with a clear error.

## Design + review trail

- Design plan: \`plans/clump-only/PLAN.md\` (438 lines, 12 resolved decisions, 3 documented deviations).
- Dual \`plan-reviewer\` round: both APPROVE WITH REVISIONS; findings incorporated into PLAN.md before implementation.
- Dual \`code-reviewer\` round + \`plan-manager\` coverage audit: 1 HIGH (panic bug) + 5 medium/low findings, all addressed. 4 further findings deferred as v1.1 with rationale.
- Verification passed locally: \`cargo build --release\`, \`cargo fmt --all -- --check\`, \`cargo clippy --all-targets --release -- -D warnings\`, \`cargo test --release\` (386 tests, 0 failures).

## Test plan

- [x] 11 new unit tests in \`src/clump_only.rs\` (permutation, PE lockstep, cross-run determinism, no-trimming, no-adapter-detection, empty input, single record, plain output, report-filename discipline, plus-line normalization, CRLF normalization)
- [x] 12 new integration tests spawning the built binary against \`test_files/BS-seq_10K_R{1,2}.fastq.gz\` (SE + PE byte-identity, \`--dont_gzip\`, cross-run determinism, report filename, rejection-matrix guards for \`--length\`/adapter/\`--rename\`, uBAM-input rejection, silent-accept guards for \`-q\`/\`--stringency\`/\`-e\`)
- [x] 3 new CI byte-identity + determinism steps in \`.github/workflows/ci.yml\` (SE + PE via \`paste - - - - | sort\`, cross-run md5 diff)
- [x] Full CI matrix green
- [ ] Docs live on \`www.trimgalore.com/modes/clump-only/\` after \`dev\` deploy

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edc8434f2d89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.