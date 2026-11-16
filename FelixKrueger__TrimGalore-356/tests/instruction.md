# Issue

**Title:** feat(clump-only): add uBAM in/out support (v2)

## Description

Stacks on top of #355 (v1 FASTQ, in-flight against \`dev\`). Delivers the uBAM in/out follow-up promised to @wkgardner in #353.

## Summary

Extends the v1 \`--clump_only\` lossless reorder mode with unaligned BAM (uBAM) support via \`--output-format ubam\`, matching the trim path's existing uBAM support. Byte-identity of record contents (id + sequence + quality + preserved aux tags) is preserved through the reorder; \`@PG\` line is appended to output header while the input \`@PG\` chain is preserved. PE-uBAM output is ONE interleaved BAM per pair (mate-adjacent, matching samtools/Picard/fgbio convention).

## Contract

**Byte-identical across the reorder:**
- Read ID / name portion
- Sequence
- Quality string
- Aux tags (uBAM only, via \`--preserve-tags\`) — A/Z/i/f scalars round-trip losslessly; B/H rejected at BAM-read time (same as trim uBAM path)

**Added on uBAM output** (matching trim uBAM path):
- \`@PG ID:trim_galore VN:<version> CL:<invocation>\` appended per invocation; input chain preserved.

**Cross-run determinism:** record-body-identical across two runs on the same input; whole-file hashes vary only because the \`@PG.CL\` field varies. CI comparison uses \`samtools view + sort + md5\` (matches trim uBAM path's \`assert_ubam_eq\` shape).

## Composability

**Composes with:** \`--paired\` (multi-pair supported N=4, 6, … via caller-driven \`.chunks(2)\`), \`--memory\`, \`--cores\`, \`--fastqc\` (fastqc-rust reads BAM natively), \`--basename\`, \`--preserve-tags\`.

**Rejects (with clear messages):**
- \`--dont_gzip + --output-format ubam\` (hoisted to \`Cli::validate\` §3.4a — also closes a pre-existing gap on the trim uBAM path)
- Two-BAM Shape A under \`--paired\` (\`R1.bam R2.bam\` is ambiguous; use a single interleaved uBAM)
- Non-BAM Shape B (\`--paired ... --output-format ubam one.fq\`)
- Mixed-format Shape A (\`--paired R1.fq R2.bam\`)
- uBAM input on the FASTQ output path (would drop aux tags; hint routes to \`--output-format ubam\`)
- Reproducible PANIC on \`--clump_only --paired ubam.bam\` (missing \`--output-format ubam\`) — caught + fixed pre-commit by dual code-review

## Outputs

- SE uBAM: \`<stem>_clumped.bam\`
- PE uBAM: ONE interleaved \`<stem>_clumped.bam\` per pair (mate-adjacent)
- Report: \`<input>_clumping_report.txt\` (renders new format labels + conditional compression ratio + preserved-tags line)

## Design + review trail

- **Design plan:** \`plans/clump-only/PLAN_v2_ubam.md\` (551 lines, 5 §Resolved decisions + 6 post-plan-review blocking fixes locked, 10-step Implementation outline, 9-item Validation list).
- **Dual \`plan-reviewer\` round** on v2 plan: both APPROVE WITH REVISIONS; 6 blocker findings incorporated into the plan before implementation (FastQC plan-drift, false parity claim on \`--dont_gzip\`, Shape A/B guard holes, multi-pair regression risk, CLI edit-site precision, collision pre-flight).
- **Dual \`code-reviewer\` round** on the implementation: Reviewer A APPROVE WITH REVISIONS (5 critical); Reviewer B NEEDS SIGNIFICANT REWORK (1 CRITICAL PANIC + 1 HIGH aux-tag test gap + 5 non-blockers). \`plan-manager\` coverage audit: INCOMPLETE WITH MINOR GAPS (29 ✅ / 4 ⚠️ / 1 ❌). All 9 blocking + should-fix items addressed pre-commit.
- Reviews stay session-local per v1 convention; only the plan file is committed.

## Test plan

- [x] \`cargo build --release\` clean
- [x] \`cargo fmt --all -- --check\` clean
- [x] \`cargo clippy --all-targets --release -- -D warnings\` clean
- [x] **\`cargo test --release\` — 407 tests, 0 failures** (v1: 386 → v2: 407, +21 tests)
- [x] 13 new integration tests in \`tests/integration_clump_only_ubam.rs\` — SE/PE positive paths, \`@PG\` chain, all 4 rejection cases, multi-pair regression guard, PANIC regression guard, aux-tag round-trip, PE-BAM collision pre-flight, FastQC-on-BAM
- [x] Byte-identity + cross-run determinism verified locally on real fixtures (\`test_files/ubam_test.bam\`, \`test_files/ubam_paired_test.bam\`, \`test_files/ubam_test_with_tags.bam\`)
- [x] Full CI matrix green (Rust tests × 2 platforms, Reproducibility, Lint, Security, Coverage, \`Validate vs Perl TrimGalore\` + 4 new uBAM validation steps)
- [x] Docs live at https://www.trimgalore.com/modes/clump-only/ after \`dev\` deploy (post-merge of both PRs)

## Follow-ups

- Trim uBAM path FastQC-skip is a pre-existing bug called out in §Resolved decision 1's rationale. Fix is a separate small PR — the trim \`run_ubam_output_*\` functions could gain the same \`fastqc::run\` calls this PR wires into the clump-only path.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f86c0f59921`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.