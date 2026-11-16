# Issue

**Title:** perf+docs: integer max_errors (#262) + memory/IO docs

## Description

## Summary

Bundles the three open issues from @an-altosian's post-Buckberry-audit pile (#262/#263/#264) into one cleanup PR. None individually warranted a separate PR; together they retire all three.

| Issue | Type | Action |
|---|---|---|
| #262 | DISCUSSION — two tail-end perf items | **Item A** (integer-arithmetic max_errors) shipped in this PR. **Item B** (read_until vs read_line) deferred — bigger scope, ~0.75% perf for ~50-100 LOC of \`String\` → \`Vec<u8>\` ripple. |
| #263 | REPORT — memory characterization (no action) | Load-bearing findings folded into \`docs/.../threading.md\` Memory profile section (vs-other-tools comparison + read-length-not-file-size scaling property). |
| #264 | REPORT — disk I/O + cache (no action) | New \"I/O and cache behaviour\" section in \`threading.md\` — disk-bandwidth-comfortable + L3-pressure-at-cores≥16 mechanism that cleanly aligns with the existing #261 cores≤16 sweet-spot finding. |

## Code change: integer max_errors

Replaced four call sites of \`(max_error_rate * len as f64).floor() as usize\` in \`src/alignment.rs\` with integer arithmetic via a \`rate_x_million\` value cached once per function entry:

\`\`\`rust
let rate_x_million = (max_error_rate * 1_000_000.0).round() as u64;
let max_errors    = ((len as u64 * rate_x_million) / 1_000_000) as usize;
\`\`\`

**Byte-identical** to \`floor(rate * len)\` for non-negative integer \`len\` (which sequence length always is — integer division truncates toward zero, same as floor() for positives). 1e6 scaling gives 6 decimal places of precision. Win: ~0.2% wall on Buckberry, eliminates the per-read libm \`floor()\` symbol that pprof attributed at 0.21% leaf self-time.

Two functions affected (\`find_3prime_adapter\`, \`myers_proves_no_match\`), four call sites total. Determinism is *better* than the floor() form — no f64 rounding-mode dependency.

## Docs additions

\`docs/.../performance/threading.md\` gains:

1. **Memory profile** section: a paragraph contextualising TG v2's <100 MB peak vs Cutadapt 100-300 MB / fastp 100+ MB / BBDuk 1-4 GB; plus the 'peak RSS scales with read length, not input file size' property with concrete 1M-50bp (28 MB) vs 84M-150bp (92 MB) datapoints.

2. **New 'I/O and cache behaviour' section** between Memory profile and Beyond speed — bandwidth-comfortable at all cores, L3-pressure mechanism behind the cores≥16 plateau, capped with the practical recommendation: \`--cores 8\` sweet spot, \`--cores 16\` upper end of useful parallelism.

Both #263 and #264 are author-marked \"no action requested\" — folding the load-bearing numbers into permanent docs ensures the data ships to readers, rather than living only in closed issues.

## Test plan

- [x] \`cargo build --release\` clean
- [x] \`cargo test --release --lib alignment\` all 20 alignment tests pass — byte-identity invariant holds
- [x] \`cargo test --release\` full suite expected green (CI on this PR will confirm)
- [x] \`npm run build\` — docs site builds with the new section
- [ ] CI green on the PR (Lint / Rust Tests / Coverage / Reproducibility / Validate-vs-Perl / Security audit)
- [ ] After merge: live www.trimgalore.com picks up the threading.md additions on next dev push
- [ ] Close #262, #263, #264 with thank-you comments referencing this PR

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `37dbc04787fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.