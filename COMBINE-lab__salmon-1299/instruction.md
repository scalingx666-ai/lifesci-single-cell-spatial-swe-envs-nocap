# Issue

**Title:** fix(cli): warn that the alignment error model flags do nothing under --rad

## Description

## Problem

`--rad` warns about most flags it cannot honour, but `--errorModel`, `--noErrorModel` and `--numErrorBins` were accepted with no message and no effect. A RAD holds no CIGARs or base qualities, so there is nothing for the alignment error model to score. A user asking for it got exit 0 and a result without it.

Reads mode already warns about the same three flags, so only `--rad` was silent.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line: "`--rad` and `-a` ignore some flags without warning." Tracked in #1283.

The audit named no flags, so I checked all of them. I ran each `salmon quant` flag once under `--rad` and once under `-a` on a synthetic paired dataset, and listed those that printed no warning and left `quant.sf` identical. Then I read each one's handling in `run_quant` to separate the flags that are really ignored from those with effects this check cannot see, such as `--numBootstraps`, or that do nothing on this data, such as `--incompatPrior`.

## Fix

One more `warn_inert_in_mode` call in the `--rad` branch for the three error-model flags.

## What was checked and left alone

- **`-a`:** no flag was found that is really ignored without a warning. So the audit's claim about `-a` did not hold up in this check, and this PR changes nothing there.
- **`--rad --initUniform`:** not forwarded, but a RAD requant already starts uniform, as the flag's own help describes for reads mode, so nothing the user asked for is lost.
- **Bias tuning flags (`--numGCBins` and similar):** these are forwarded, and do nothing here only because no bias model ran in this check.

## Limits

The check used one small dataset and flag values picked by hand, and it judged by reading the code wherever `quant.sf` did not change. A flag whose handling I misread would be missed.

## Behaviour change

A warning only. Results do not change.

## Verification

- `mode_applicability` now passes the two flags under `--rad` and asserts the warning; `mode_applicability` and `flag_matrix` pass, and clippy is clean.
- The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.