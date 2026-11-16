# Issue

**Title:** fix(infer): sum a gathered step's L1 as a pushed step does

## Description

## Problem

The Projected stop rule decides when a component stops from the L1 size of each step, and `run_projected` documents that the result is independent of the thread count. It is not quite, for large components:

- `-p 1` steps a component with `step_push`, whose L1 is one flat sum over its transcripts.
- `-p N` steps a component with at least 2^16 incidences with `step_pull`, whose L1 is summed per chunk of 2048 transcripts and then added up.

Float addition is not associative, so these differ in the last bits. On a 6,001-transcript component, the first three steps gave:

```
push: [4698800388014676659, 4678675914660442110, 4676202748881284640]
pull: [4698800388014676685, 4678675914660442124, 4676202748881284629]
```

The comment on that code says the sum "does not depend on the thread count". That holds between thread counts greater than 1, because the chunks are fixed. It does not hold between `-p 1` and `-p N`, which is the comparison that matters. If `l1 / (1 - rho) < PROJECTED_EPS * mass` falls within that rounding error, the two runs stop one iteration apart and the abundances differ.

The existing test `projected_stop_is_independent_of_threads_and_stepping` could not see this: its components have far fewer than 2048 transcripts, so there is only one chunk.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line: "The Projected stop rule can differ by a rounding error between `-p 1` and `-p N`." Tracked in #1283.

## Fix

`step_pull` keeps its parallel per-chunk work for the criterion, and computes L1 in one serial pass over `alpha` and `next`, in the same order as `criterion`.

## Behaviour change

A large component under `-p N` now gets exactly the L1 that `-p 1` gets. Whether any real run's output changes depends on the stopping test landing inside the rounding error, so most runs will not change.

## Cost

One more serial pass over a large component's transcripts per step. That pass is plain subtraction and addition, next to a step that already does much more work per incidence (components here have at least 2^16). I did not time it: the machine was under heavy load, so a timing would not have meant much.

## Limits

I did not produce a whole run whose `quant.sf` differs between `-p 1` and `-p N`. A check on 120,000 synthetic reads gave byte-identical results at 17 significant digits on `develop`, but its components are too small to use `step_pull`. The evidence is the step-level difference above, and that the stopping test reads this value.

## Verification

- The new test `a_gathered_step_of_a_large_component_has_the_same_l1_bits` failed before the fix with the numbers above, and passes now.
- The `components::` unit tests pass, and clippy is clean. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.