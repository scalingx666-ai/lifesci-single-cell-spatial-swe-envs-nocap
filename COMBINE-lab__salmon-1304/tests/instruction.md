# Issue

**Title:** fix(core): resolve --ignoreTxVersion collisions independently of hash order

## Description

## Problem

With `--ignoreTxVersion`, the gene map is re-keyed with versions stripped. If two versions of a transcript belong to different genes, they collapse onto one key, and the winner was whichever `HashMap` iteration visited last. Rust's hash order is randomised per process, so **the same command on the same input gave a different gene from run to run**.

A gene map with `t.1 -> G1` through `t.8 -> G8`, and one quantified transcript `t.9`, run 25 times:

| | `quant.genes.sf` row |
|---|---|
| before | G2 ×8, G8 ×7, G1, G4, G5, G7 ×2 each, G3, G6 ×1 each |
| after | G1 ×25 |

Nothing warned about the collision, and the default mode otherwise promises one answer for one input.

An exact match also lost out: with `--ignoreTxVersion`, a quantified `t.2` could join to `t.1`'s gene even though the map has `t.2`.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line: "`--ignoreTxVersion` collisions depend on hash order." Tracked in #1283.

## Fix

- The map is walked in sorted order when re-keying, so the lowest identifier wins.
- An exact name match is tried first, so `t.2` joins to `t.2`'s gene.
- `GeneQuantSummary::version_collisions` counts entries that disagree with an earlier version of the same transcript, and the CLI warns when it is above zero. Versions of a transcript that agree on the gene are not counted.

## Behaviour change

Only `--ignoreTxVersion` runs on a gene map with such collisions change: they get a fixed answer and a warning. "Lowest identifier" compares strings, so `t.10` sorts before `t.9`. It is a stable rule rather than a claim about which version is right, and the warning says so.

## Verification

- The new test `ignore_tx_version_resolves_a_collision_independently_of_hash_order` covers the exact match, the fallback to the lowest identifier, and the count.
- The table above comes from running a build of `develop` and this branch 25 times each.
- Tests of `salmon-core` pass, and clippy is clean. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.