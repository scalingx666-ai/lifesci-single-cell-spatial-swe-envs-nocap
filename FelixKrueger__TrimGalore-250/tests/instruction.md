# Issue

**Title:** perf: Buckberry-scale wins #2 + #1 from #248 (co-authored with @an-altosian)

## Description

## Summary

Lands two of the three confirmed performance wins from @an-altosian's Buckberry-scale audit (#248). Item #4 (Myers' bit-parallel adapter alignment) is queued for a separate PR from him — his Buckberry-validated reference implementation isn't on his public fork branches, so we're letting him drive that one to preserve the byte-identity guarantees he's already verified.

## Commits in this PR

| Commit | What | #248 item | At-scale Δ |
|---|---|---|---:|
| \`4712bd8\` | \`perf(fastq)\` — single buffered write per FASTQ record | **#2** | **~−10%** wall |
| \`6a6de49\` | \`perf(gzip)\` — lower default output compression level 6 → 1 | **#1** | **~−23%** wall |
| \`ceb2385\` | \`docs(readme)\` — note level-1 gzip default + size trade-off | (follow-up) | — |
| \`d6d29f4\` | \`docs(credits/changelog)\` — Buckberry perf wins + recognise Dongze + Phil | — | — |

Both wins are co-authored with @an-altosian — \`Co-authored-by:\` trailers on every commit, and a Contributors section added to the docs site (\`reference/credits.md\`) recognising his Phase-1B Perl-parity hunt and the Buckberry-scale audit.

## What changes for users

**#2 (single buffered write)** is byte-identical to the previous output. Same input → same output bytes. End-to-end md5 verified on \`BS-seq_10K_R1\` (\`12fde5c81a6780ecfa57e54b7953894a\` matches before and after).

**#1 (gzip 6 → 1)** is byte-identical *after \`gzip -d\`* — same decompressed content, different gzip framing. The trade is **output \`.fq.gz\` files are roughly 75% larger** in exchange for substantial wall-time reduction (~23% at Buckberry scale, cores=8). Locally measured: 273 KB → 479 KB on \`BS-seq_10K_R1_trimmed.fq.gz\`.

The CI \`validation\` job's md5 oracle uses \`gzip -dc | md5sum\` everywhere, so it continues to compare decompressed content against Perl v0.6.11 — and continues to pass on every flag path (single-end, paired-end, multi-pair PE, retain-unpaired multi-pair, hardtrim5, clock, demux). Verified locally.

A future \`--high-compression\` opt-in flag for storage-conscious pipelines would be a one-line edit at the new \`pub const OUTPUT_GZIP_LEVEL\` in \`src/fastq.rs\`. Keeping that as a separate decision.

## Verification

- [x] \`cargo test --release\` — 177 passed, 0 failed
- [x] \`cargo fmt --all -- --check\` — clean
- [x] \`cargo clippy --all-targets --release -- -D warnings\` — clean
- [x] End-to-end smoke for #2: md5 of decompressed trimmed output matches pre-change baseline byte-for-byte
- [x] End-to-end smoke for #1: md5 of decompressed trimmed output matches level-6 baseline; \`.fq.gz\` size +75.1%
- [x] Docs site builds (28 pages, no warnings)
- [ ] Validation matrix runs green on this PR — particularly important for #1 where the gzip framing changes
- [ ] Buckberry-scale wall-clock reproduction is out of scope for CI; @an-altosian's hyperfine recipe in #248 stays the canonical performance source

## What's NOT in this PR

- **#248 item #4** (Myers' bit-parallel adapter alignment, ~−13% additional wall-time at byte-identity). His reference implementation lives on an ephemeral worktree branch on his fork that's no longer reachable; reimplementing from scratch carries real algorithmic risk. Letting him send that PR.

Addresses #248

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `76a58def37ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.