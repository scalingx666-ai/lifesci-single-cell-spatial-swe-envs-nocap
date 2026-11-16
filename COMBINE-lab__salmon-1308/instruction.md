# Issue

**Title:** perf(quant): add to the shared processed count once per batch

## Description

## Problem

Every worker did `fetch_add` on the shared `num_processed` once per fragment. A relaxed increment is cheap in itself, but all workers write the same cache line, and the cost grows with `-p`. `Counters` was introduced to remove exactly this cost for the other tallies, and its doc comment says so.

That comment gave one reason to leave `num_processed` shared: it "is also *read* on the hot path, to gate `use_aux`". That stopped being true with #1089, which moved the gate to the count of assigned fragments. Nothing reads `num_processed` during the pass any more, apart from the progress display.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line: "`num_processed` is a shared counter updated per fragment that could be updated per batch." Tracked in #1283.

## Fix

`Counters::processed` counts privately, and `flush_processed` adds it to the shared total at the end of each batch, in both the paired and the single-end processors. Per batch rather than per thread, so the progress display stays live. The stale comments are updated.

## Behaviour change

None in results. The spinner's processed count now moves once per batch per worker.

## Limits

- No speed-up is claimed. I did not time this: the machine was under heavy load, and the gain only shows at high thread counts.
- `num_mapped` stays shared per fragment. Its comment makes the same claim about gating `use_aux`, which looks stale too, but it was outside this finding and I did not check it.

## Verification

- `num_processed`, `num_mapped` and the `quant.sf` hash match a build of `develop` on 30,001 fragments, a third of them unmapped, for paired and single-end, with and without `--online`.
- Tests of `salmon-quant` and `salmon-cli` pass, and clippy is clean. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.