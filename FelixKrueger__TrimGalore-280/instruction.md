# Issue

**Title:** docs/cli: align --cores guidance on N+4 model and 8-core saturation

## Description

## Summary

Three coordinated edits replacing the older \"near-linear through 16 cores; diminishing beyond ~20\" framing with the v2.1.0-beta.7+ Buckberry-derived story (N+4 thread model + paired-end saturation around \`--cores 8\`).

| File | Change |
|---|---|
| \`src/cli.rs\` (\`--cores\` doc-comment) | Rewrite so \`trim_galore --help\` explicitly names the N+4 thread model (N workers + 2 decompressors + 1 batcher + 1 writer) and near-linear-to-8 PE speedup, with the gzip-output I/O caveat for higher core counts. |
| \`docs/.../performance/threading.md\` | Keep the cores=1 bypass note, but fold N+4 + 8-core saturation into the same paragraph so readers see the full picture before the efficiency table that follows. |
| \`README.md\` (Parallel-processing feature bullet) | Tighten \"near-linear speedup on multi-core systems\" to the same N+4 + 8-core saturation framing. |

## Test plan

- [x] \`cargo build --release\` clean
- [x] \`trim_galore --help\` renders the new text correctly
- [x] \`npm run build\` produces 28 pages clean
- [ ] CI green on the PR (Lint / Rust Tests / Coverage / Reproducibility / Validate vs Perl / Security audit)
- [ ] Pages deploy after merge picks up the threading.md text

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e11b54bcdd2f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.