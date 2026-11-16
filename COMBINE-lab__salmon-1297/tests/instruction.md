# Issue

**Title:** fix(quant): do not collect bias models a pass will not use

## Description

## Problem

`collect_seqbias`, `collect_gcbias` and `collect_posbias` were set from the bias flags alone, while the shared models that receive the results are gated on `observe_bias` too (`!skip_quant` and length correction on). So a `--skipQuant` pass with `--seqBias`, which includes phase 1 of a default single-end run, gave each worker its own pair of `SBModel`s, updated them for fragments on the mapping path, and then dropped them: `seqbias_obs` is `None`, so the merge at the end of the worker has nowhere to put them.

The comment above `observe_bias` already says this work should not happen on such a pass. It was removed for the shared models, but not for the per-worker ones.

Paired runs in phase 1 go through `record_discrete` and skip this path.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line: "`--seqBias` updates a model that is then thrown away." Tracked in #1283.

## Fix

Each `collect_*` flag is now `*_obs.is_some()`, so a worker collects exactly when something will receive the result. The audit named `--seqBias`; the GC and positional flags had the same mismatch and get the same one-word change.

## Behaviour change

None in results. I compared `quant.sf` from a build of `develop` with this branch on a synthetic single-end dataset (150,000 reads, `-l A`), with no bias flag, each bias flag alone, and all three: byte-identical in all five cases.

## Limits

No new test: nothing outside the worker can see the dropped model. I timed the `--skipQuant` pass too, but on a debug build and a busy machine the differences were within noise, so this PR claims no measured speed-up.

## Verification

- The `quant.sf` comparison above.
- Tests of `salmon-quant` pass. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.