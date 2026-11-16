# Issue

**Title:** fix: Perl-parity bundle (#242, #245, #246, #247) + #243 UX polish

## Description

## Summary

Bundles six commits closing or partially-closing five issues raised during @an-altosian's Phase-1B Perl-parity hunt. All commits are independently scoped and individually revert-clean if any one needs to be backed out post-merge.

## Commits in this PR

| Commit | What | Issue |
|---|---|---|
| \`110c199\` | \`fix(cli)\` — accept lowercase clip-flag spellings (\`--clip_r1\` etc.) | **#242** |
| \`832e2ea\` | \`feat(cli)\` — warn when \`--max_n\` enters fraction mode (Perl parity) | **#243** |
| \`e5bf8fc\` | \`fix(cli/filters)\` — Perl-parity for output gzip + \`--retain_unpaired\` | **#245** items A, C, D |
| \`68bb475\` | \`docs(readme)\` — note that output compression mirrors input | (-A) |
| \`4605e8e\` | \`test(coverage)\` — close 5 of 6 §5.x items from the test-coverage audit | **#246** items §5.1, §5.3, §5.4, §5.5, §5.6 |
| \`d7b3f6c\` | \`ci\` — hardening: failure artifacts + local Perl source + Cutadapt rev pin | **#247** items 1, 5, 6 |

## Highlights

**Real Perl-parity bugs fixed**:
- Lowercase clip-flag spellings now accepted (every Perl-era pipeline using \`--clip_r1\` was broken under v2.x).
- Output gzip mirrors input compression by default (plain in → plain out, .gz in → .gz out). \`--dont_gzip\` still forces plain.
- \`--retain_unpaired\` now correctly routes both mates to their unpaired files when both fail \`--length\` but each is individually long enough for \`--length_{1,2}\`.

**UX warnings added**:
- \`--max_n 0.5\` now logs the same notice Perl prints, so users can see at runtime which mode they're in.

**Test coverage**:
- \`demux.rs\` zero-tests gap closed (CRLF samplesheet handling + short-read NoCode routing).
- \`fastq.rs\` multi-member gzip round-trip regression test (covers a pre-beta.1 fix that never had a unit test).
- \`adapter.rs\` 1M-read scan-limit boundary verified at scale 7 via a crate-private \`autodetect_adapter_with_max_scan\` helper.
- \`report.rs\` PE param-summary \`removed-end:\` typo class locked down for MultiQC parsers.
- Total tests: 165 → 177.

**CI hardening**:
- \`if: failure()\` artifact upload on the validation job — md5 mismatches now surface the actual outputs as a downloadable artifact.
- Perl Trim Galore source fetched from local \`origin/master\` instead of curling \`raw.githubusercontent\` — no external network dependency.
- Cutadapt bioconda revision pinned to \`5.2=*_0\` so an unannounced rev bump can't silently shift the validation matrix's md5 baseline.

## Items deliberately deferred

Each of these is tracked on the source issue and warrants a focused PR of its own:
- **#245 item B** — \`-a 'A{15}'\` adapter-alignment difference on highly-repetitive patterns (brace expansion is correct; the divergence is in the alignment DP tolerance, separate investigation).
- **#246 §5.2** — parallel/serial \`TrimStats\` parity (needs harness scaffolding to expose stats from a parallel run).
- **#246 module-gap** — comprehensive \`parallel.rs\` unit-level coverage.
- **#246 bonus** — upstreaming @an-altosian's \`tests/parity_proptest.rs\` harness.
- **#247 item 2** — macOS runner in \`rust-tests\` (doubles wall time).
- **#247 item 3** — \`cargo test --release\` step.
- **#247 item 4** — coverage reporting (cargo-llvm-cov / tarpaulin).
- **#247 item 7** — \`justfile\` for local CI parity.
- **#247 item 8** — \`cargo nextest\` adoption.
- **#248** — three confirmed perf wins (gzip-level, single buffered write, Myers' alignment); deferred entirely to await @an-altosian's incoming PRs (#2 → #4 → #1 in his stated order).

## Test plan

- [x] \`cargo test --release\` — 177 passed, 0 failed
- [x] \`cargo fmt --all -- --check\` — clean
- [x] \`cargo clippy --all-targets --release -- -D warnings\` — clean
- [x] YAML \`ci.yml\` parses (\`python3 -c 'import yaml; yaml.safe_load(open(...))'\`)
- [x] End-to-end smoke for the parity fixes:
  - \`--clip_r1 5\` parses correctly
  - Plain \`.fastq\` input → plain \`.fq\` output; \`.fastq.gz\` input → \`.fq.gz\` output; \`--dont_gzip\` overrides
  - \`--paired --retain_unpaired --length 80\` populates both \`_unpaired_*.fq.gz\` files (~9996/10000 records each on \`BS-seq_10K\`)
  - \`--max_n 0.5\` emits the fraction-mode warning to stderr
- [ ] Validation matrix runs green on this PR — particularly important for the CI changes (item 5 \`git show origin/master:trim_galore\` and item 6 Cutadapt \`*_0\` pin)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56734db923c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.