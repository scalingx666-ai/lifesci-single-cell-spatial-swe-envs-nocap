# Issue

**Title:** ci: backfill coverage for retain_unpaired × multi-pair, missing inputs, report-path fail-fast

## Description

## Summary

Pre-GA nit-PR closing the three CI coverage gaps Reviewer A flagged during the multi-pair PR review. All CI-only changes — no source code touched, no behaviour change. These are existing behaviours that simply weren't being exercised.

- **Tightened collision fail-fast assertions** — both collision pre-flight tests used \`test -z \"\$(ls .../out/*.fq.gz)\"\`. Changed to \`test -z \"\$(ls -A .../out)\"\` so any write (trimming reports, JSON reports, FastQC outputs) before the bail now fails the test, not just FASTQ files.
- **New \`--retain_unpaired × multi-pair\`** positive test — exercises the \`retain_unpaired\` branch of the collision pre-flight (\`src/main.rs:101-111\`) and confirms per-pair unpaired file naming (\`{sample}_R1_unpaired_1.fq.gz\` + \`{sample}_R2_unpaired_2.fq.gz\` for each of two pairs). Uses \`--length 80\` to force reads into the unpaired bucket.
- **New \`missing input mid-list\`** negative test — 3-pair invocation with pair B's R1 absent. Asserts exit≠0, error message \`Input file not found\`, AND that earlier-listed pair A was NOT processed before \`Cli::validate()\` caught the missing input. Proves fail-fast ordering of the existence check.

## Test plan

- [x] Locally verified \`--retain_unpaired\` multi-pair produces all four expected unpaired files per pair (\`A_R1_unpaired_1.fq.gz\`, \`A_R2_unpaired_2.fq.gz\`, \`B_R1_unpaired_1.fq.gz\`, \`B_R2_unpaired_2.fq.gz\`).
- [x] Locally verified missing input mid-list errors with \`Input file not found: /tmp/.../B_R1.fastq.gz\` and writes no outputs.
- [ ] CI green on all 5 gates (lint, reproducibility, tests, audit, Perl validation).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aab53aeec2e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.