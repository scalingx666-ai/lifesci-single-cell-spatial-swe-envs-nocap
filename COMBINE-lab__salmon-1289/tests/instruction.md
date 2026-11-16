# Issue

**Title:** fix(model): apply the effective-length floor on the cross-correlation path

## Description

## Problem

The bias correction floors effective length at a lower barrier, `min(elen, max(1, unprocessed))`, because a too-small length inflates abundance. A transcript shorter than every fragment length has nothing to convolve, so only that floor decides its length. The two code paths disagreed on it:

| Path | Used by | Result for a 120 nt transcript, `elen` 75 |
|---|---|---|
| Cross-correlation (`eff_len_from_xcorr`) | `--seqBias`, `--posBias` | 75 |
| Scalar convolution | any run with `--gcBias` | 45 |

The cross-correlation path returned early with `elen.max(elen.min(offset))`, which always equals `elen`, so its floor did nothing. TPM divides by this length, so the same transcript differed by about 1.67× depending on which bias flag was on.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit read the expression and saw it could never differ from `elen`. It did not run this case. The new test measures it directly, on `corrected_effective_length_full`, and gives the 75 and 45 above. Tracked in #1283 (finding 18).

## Fix

Delete the early return in `crates/salmon-model/src/seqbias.rs`. With no length to sweep, the loop below does nothing, and the same floor code as the normal path runs. That code also honours `no_length_threshold`, which the early return ignored.

## Behaviour change

This changes results. Transcripts shorter than the fragment-length range, under `--seqBias` or `--posBias` without `--gcBias`, get the lower length, so their TPM rises. I took the scalar path as the right answer because the doc comments on the correction functions describe that barrier. Please confirm that's the intended one.

## Limits

I did not run a benchmark with known true values, which the audit suggested for this finding.

## Verification

- New test `short_transcript_floor_is_the_same_on_every_bias_path` in `crates/salmon-model/src/bias.rs`. I saw it fail without the fix (`75` versus `45`). It calls the production entry point with positional and GC inputs. The `--seqBias` input takes the same cross-correlation path, but the test does not exercise it separately.
- `salmon-model`, `salmon-align` and `salmon-cli` tests pass, and workspace clippy is clean with `-D warnings`. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.