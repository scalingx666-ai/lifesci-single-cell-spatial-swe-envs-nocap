# Issue

**Title:** fix(cli,index): refuse out-of-range numeric flags and an impossible k or m

## Description

## Problem

Several numeric inputs reached the run unchecked, so a typo gave wrong numbers or a late crash rather than an error.

| Input | Before | After |
|---|---|---|
| `--vbPrior NaN` | exit 0, 6931 of 10000 reads kept (audit run) | refused by the parser, exit 2 |
| `--fldMax 0` | TPMs change, no warning (audit run) | refused by the parser, exit 2 |
| `index -k 33` | panic in `tiny-dict`, exit 101, 12 files left in the index directory | refused, exit 1, nothing written |
| `index -k 21 -m 25` | exit 1, 7 files left in the index directory | refused, exit 1, nothing written |

The index check accepted any odd k up to 63, but `tiny-dict` asserts `K <= 31`. The `-m` check existed only deep in the build.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit passed bad values to these flags and read the results. I re-measured the index rows on `develop`; the `--vbPrior` and `--fldMax` numbers come from the audit's run. Tracked in #1283 (finding 15).

## Fix

- **`salmon-index`:** `build` requires an odd k of at most 31 and `m < k` before it creates the output directory. The check covers every caller, not only the CLI.
- **`--vbPrior`:** reuses `parse_positive_f64`.
- **`--fldMax`:** must be at least 1.
- **New parsers for the other float flags, which took any value including `NaN`:**

| Allowed range | Flags |
|---|---|
| `[0, 1]` | `--incompatPrior`, `--minAlnProb`, `--minScoreFraction`, `--orphanChainSubThresh`, `--consensusSlack`, `--preMergeChainSubThresh`, `--postMergeChainSubThresh` |
| at least 0, finite | `--scoreExp`, `--decoyThreshold`, `--juncMissDiscount` |
| `(0.5, 1.0]`, as its help already says | `--forgettingFactor` |

## Behaviour changes

Runs with these values used to proceed and now fail. Please check these ranges in particular:

- **`-k` above 31** is now an error. No valid index could be built that way, and the `-k` help now says "at most 31".
- **`--vbPrior 0`** is refused, since `parse_positive_f64` requires more than 0. If a zero prior is meant to work, this parser should be relaxed.
- **`--incompatPrior` above 1** is refused, because it would reward wrong-strand mappings.
- **The upper bound on the `[0, 1]` flags** comes from their help text or their use as a fraction. Only the pre- and post-merge flags state it outright.

## Limits

`--fldMax` has only a lower bound: a small value such as 10 is still accepted. Integer flags other than `--fldMax` were not reviewed.

## Verification

- New tests in `crates/salmon-cli/tests/input_validation.rs`: `numeric_flags_out_of_range_are_refused` and `an_impossible_k_or_m_is_refused_before_writing_anything`. I saw both fail without the fix (exit 1 for `--vbPrior NaN`, exit 101 for `-k 33`).
- `salmon-cli` and `salmon-index` tests pass, and workspace clippy is clean with `-D warnings`. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.