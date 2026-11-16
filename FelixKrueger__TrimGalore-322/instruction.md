# Issue

**Title:** fix(poly-g): trim R2's 3' poly-G tail (was incorrectly 5' poly-C)

## Description

## Summary

Fix for  (reported by @K81ta).

The 2-colour poly-G artifact is **sequencer-induced** (the instrument calls "no signal" as a high-quality G when it overruns the template), and it manifests at the **3' end of every read regardless of strand orientation**. The original code copied the poly-A `revcomp = is_r2` cross-strand pattern — correct for poly-A (template-side: mRNA tail on the forward strand → R1 sees 3' poly-A, R2 sees 5' poly-T in reverse-complement), wrong for poly-G (sequencer-side, hits 3' of both reads).

Net effect of the bug: R2's actual 3' poly-G tail went untrimmed; instead `--poly_g` ate legitimate 5' poly-C content on R2.

## Behaviour change

- ✅ R2 records with 3' poly-G tails are **now trimmed** (previously untouched — this was the bug)
- ✅ R2 records with legitimate 5' poly-C content are **no longer eaten** by \`--poly_g\` (this was the buggy side-effect)
- ✅ R1 / single-end behaviour: **unchanged** (only the R2 path differed)
- ✅ \`--poly_a\` / poly-T behaviour: **unchanged** (still template-side, still cross-strand on R2 — correct as it was)
- ✅ v0.6.x Perl byte-identity: **unaffected** (\`--poly_g\` is a v2.x-only feature; confirmed via \`git show 0.6.11:trim_galore | grep poly_g\` → zero matches)

## Files changed

- \`src/trimmer.rs\` — fix the poly-G branch (drop the \`revcomp = is_r2\` line; always trim 3'); + 3 new lib regression tests
- \`src/main.rs\` — paired summary lines: "R2 reads with poly-C trimmed" → "poly-G"
- \`src/report.rs\` — \`TrimStats\` field docs + report-header text
- \`README.md\` — feature bullet rewritten
- \`docs/src/content/docs/modes/poly.md\` — dedicated prose updated to reflect 3'-both-reads + the why
- \`CHANGELOG.md\` — fix entry under Unreleased

## Test plan

- [x] \`cargo test --release\` — 353 tests pass (+3 over 350 baseline)
- [x] \`cargo fmt --all -- --check\` clean
- [x] \`cargo clippy --release --all-targets -- -D warnings\` clean
- [x] Manual: \`test_poly_g_r2_trims_3prime_tail\` — R2 with \`...GGGGGGGGGGGG\` 3' tail → 12bp removed from 3'
- [x] Manual: \`test_poly_g_r1_still_trims_3prime_tail\` — R1 regression guard, same outcome
- [x] Manual: \`test_poly_g_r2_does_not_trim_5prime_poly_c\` — confirms the old buggy 5' poly-C eating is gone
- [ ] CI: Perl 0.6.11 byte-identity for the FASTQ output path stays green (sanity — should be unaffected since poly-G is v2-only)
- [ ] CI: existing poly-A / poly-T tests stay green (sanity — only the poly-G branch changed)

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a976fecb7aee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.