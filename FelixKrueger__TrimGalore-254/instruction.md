# Issue

**Title:** chore(release): v2.1.0-beta.6 — Perl-parity bundle + Buckberry perf wins + CI hardening

## Description

## Summary

Cuts \`v2.1.0-beta.6\`. Bumps \`Cargo.toml\` 2.1.0-beta.5 → 2.1.0-beta.6, dates the CHANGELOG section, and updates the forward-looking install pins in \`README.md\` + the docs site's install page.

## What's in v2.1.0-beta.6

**Bug fixes (Perl-parity, contributor-reported by @an-altosian)**:
- #242 lowercase clip-flag spellings (\`--clip_r1\` etc.) accepted
- #244 \`--basename foo --paired\` → \`foo_val_{1,2}.fq.gz\` (no \`_R{1,2}\`)
- #245-A output gzip extension mirrors input compression
- #245-C \`--retain_unpaired\` routes both mates independently to unpaired
- #245-D \`--clock\` / \`--implicon\` imply \`--paired\` (intentional widening)

**Other bug fixes**:
- \`-o/--output_dir DIR\` no longer hangs when \`DIR\` doesn't exist (parallel path was deadlocking)
- #232 RRBS \`Total written (filtered)\` cutadapt-section line matches Perl byte-for-byte
- #233 \`RUN STATISTICS\` filter-removed lines emitted at zero count
- #234 four trimming-report shape changes documented as migration notes

**UX**:
- #243 \`--max_n\` fraction-mode logs the Perl-style notice on entry

**Performance** (Buckberry-scale audit, #248 — co-authored with @an-altosian):
- #248 #1 output gzip compression level 6 → 1 (~−23% wall, +75% size)
- #248 #2 single buffered write per FASTQ record (~−10% wall)
- (#248 #4 Myers' bit-parallel adapter alignment is queued for a separate PR from him)

**Tests** (#246 — closed 5 of 6 §5.x items): 165 → 180 unit tests.

**CI hardening** (#247): macOS matrix on \`rust-tests\`, release-profile test step, \`coverage\` job via \`cargo-llvm-cov\`, \`failure()\` artifact upload on validation, local \`git show\` instead of curl for Perl source, Cutadapt rev pinned, top-level \`justfile\` for local CI parity.

## Verification

- [x] \`./target/release/trim_galore --version\` reports \`trim_galore 2.1.0-beta.6 (Oxidized Edition)\` ✓
- [x] 180 tests pass on the bumped \`Cargo.toml\`
- [x] \`cargo fmt\` + \`cargo clippy --all-targets --release -- -D warnings\` clean
- [x] No remaining forward-looking \`2.1.0-beta.5\` references (the three preserved are intentional historical comments)
- [ ] CI on this PR exercises the new matrix entry, coverage job, and validation matrix
- [ ] Post-merge: \`gh workflow run release.yml --ref optimus_prime\` to actually publish (release.yml gates artifacts on \`workflow_dispatch\`; push-only goes green but skips them silently)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ae3cb190fde`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.