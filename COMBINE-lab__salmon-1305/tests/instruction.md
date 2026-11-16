# Issue

**Title:** fix(infer): at the iteration cap, blame only the components still changing

## Description

## Problem

Under `--stopRule global`, a run that reached the iteration cap reported **every** connected component as stuck: `num_unconverged` and `num_at_max_iter` were set to the total component count, and `reads_at_max_iter` to all reads. So `fraction_reads_at_max_iter` in `meta_info.json` was always 1.0 at the cap, and the run log said that all N components "never met the convergence criterion".

One slow component among thousands is enough to make the whole run report that. The numbers are only useful if they say how much of the data is affected, which is what the Projected rule already reports.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line: "A global-rule run at the iteration cap blames every component." Tracked in #1283.

## Fix

Each component already records whether its own criterion failed on its last step (`CompState::changed`), because the tiled loop uses that to pick its witness. The summary now counts only those components and their reads.

No extra work is done on the EM path, and the estimates do not change: this only reads state the loop already kept.

## Behaviour change

`em_components` in `meta_info.json` and the log line, for a global-rule run stopped by the cap. A run that converges reports zeros as before. `converged` is unchanged.

## Limits

If `max_iter` were below `min_iter`, the run could end with `converged: false` and zero components blamed, because every criterion held and only the minimum was unmet. Those are not values a user can set from the command line today.

## Verification

- The new test `a_capped_global_run_blames_only_the_unsettled_component` has two components, stopped at 6 iterations: one is blamed, with its 90 fragments, not both with all 100,170.
- The `components::` unit tests pass, and clippy is clean.
- I did not get a full `salmon-infer` run. The machine was under heavy load, and `daarem_em_stops_as_close_as_plain_em` was still running in a debug build when a 400 s limit stopped it. That test does not touch this code. The whole workspace suite was not run on this branch either; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.