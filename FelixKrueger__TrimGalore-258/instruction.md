# Issue

**Title:** perf(alignment): Myers' bit-parallel prefilter (#248 #4, byte-identical, co-authored)

## Description

Lands the third and final perf win from @an-altosian's #248 Buckberry-scale audit.

Implements Myers' bit-parallel approximate matching (Hyyrö 2001 formulation) as a **prefilter wrapped around the existing scalar DP** — the "preserves byte-identity by construction" design Dongze described in the issue body.

## How it preserves byte-identity

\`myers_proves_no_match\` is conservative: it only short-circuits when the O(n) bit-vector walk can rigorously prove that no adapter match exists, considering BOTH:

1. **Full-match case** (last DP row): tracks min_score across all read positions via the running counter on the top bit of Ph/Mh.
2. **Partial-match case** (last DP column): at end-of-walk, the bit-vectors encode dp[i][n] - dp[i-1][n] for i in 1..=m; reconstructs dp[i][n] iteratively from dp[0][n] = 0 and compares each row against the per-overlap error budget.

When either check signals "possible match", control falls through unchanged to the scalar DP which gives the canonical answer. False positives → slight perf loss, no correctness impact.

## End-to-end byte-identity verified

- BS-seq_10K_R1 trimmed-output md5 = \`12fde5c81a6780ecfa57e54b7953894a\` (same as beta.6 baseline)
- 12 existing alignment tests pass unchanged — Myers' is transparent to the existing \`find_3prime_adapter\` contract
- 8 new \`alignment::tests::myers_*\` tests cover: adapterless reads, adapter-present reads, error-budget edge, partial 3' overlap, long-adapter fall-through, 64 bp boundary, all-N reads, and a hand-picked equivalence sweep against the scalar DP
- Total: 180 → 188 tests

## Bug discovery (captured in commit message)

Two subtle bugs hit during impl, worth noting in case anyone reads the file history later:

1. The shift carry must NOT include \`| 1\` for approximate-matching (dp[0][j] = 0); that's the global-alignment boundary. Concrete test case that distinguishes: an all-mismatch first column should yield pv = m_mask, and \`| 1\` zeros bit 0.
2. Typo at the new-pv computation: must use \`xv\`, not \`xh\`. Both are valid u64s so compile + small tests passed; only the partial-match column reconstruction caught it via \`test_partial_adapter_at_3prime\`.

## Limits

Single-word u64 — adapter must be 1..=64 bp. Longer patterns fall through unconditionally. Project's adapters are ≤ 32 bp (BGI/DNBSEQ at 32 is the longest), so this is sufficient for production.

## Attribution

Profiled, prototyped, and benchmarked at Buckberry scale (84M reads, 38% adapter rate, cores=8) by @an-altosian. The wrapper-as-prefilter design is his. We tried to port the prototype but his ephemeral worktree branch (\`worktree-agent-aeb2047126268fb9e\`) was cleaned up by Claude Code's standard worktree cleanup before we could fetch it (commit \`7974ab0\` returns 422 from the GitHub API, meaning it never reached a long-lived branch). This implementation is independent but follows his stated shape exactly.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2a8f0c2ec835`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.