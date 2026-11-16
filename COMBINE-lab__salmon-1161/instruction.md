# Issue

**Title:** fix: bound bias correction by the decoy boundary, and detect it if the assumption breaks

## Description

Item 1 from your question, plus the assumption you asked to have documented.

## The bound

The one-pass reads path computes `num_targets = first_decoy_index` and passes it to all three expected-bias model builders *and* the per-reference `corrected_effective_length_full` sweep. The shared `apply_bias_correction` — used by deterministic phase 2, deterministic `-a`, `--rad` and genome projection, i.e. **every default path since 2.6.0** — passed `num_refs` to all four, guarding the sweep only on `alphas[tid] < 1e-8`. The boundary was already available there; #1153 bakes it into the RAD header and `rad.rs` loads it. It just was never threaded in.

`build_expected`'s own contract says why this matters: the abundance guard is defense in depth, the range bound is what *guarantees* "no O(refLen) decoy sweep can ever run". Without it a decoy with any abundance drags a genome-scale chromosome (up to ~250 Mb) through a single-threaded sweep of the run's dominant phase — issue #1019, fixed for one-pass by PR #1020.

**Not currently reachable, and I checked rather than assumed.** Reads mode drops decoy placements before the RAD is written, so decoys always end with alpha 0. I built the case that should trigger it — a 28 Mb decoy chromosome containing verbatim copies of 20 of 200 transcripts, the processed-pseudogene scenario decoys exist for — and measured 0.18 s default vs 0.17 s `--online` with `--seqBias --gcBias`. So this restores a guarantee; it does not fix an observed stall.

## The assumption, recorded and made detectable

You said piscem never puts decoy-mapping reads in the RAD. That's right, and by a stronger mechanism than "they're filtered": **piscem does not index decoys as references at all.** `--decoy-paths` feed `build_poison_table` in both `piscem` and `piscem-rs`, turning decoy sequence into poison k-mers used to *reject* reads — so no RAD record can point at a decoy, because decoys aren't in the reference table. `rad.rs`'s module docs claimed decoy filtering for piscem RADs was a "tracked follow-up", implying a gap that cannot exist; corrected.

Both invariants (salmon's write-time filter, piscem's poison design) are enforced upstream and invisible from the bias code, so a comment alone would rot. If either broke, the failure would be silent and nasty: TPM is normalized over every reference and rows are filtered afterward, so mass landing on an excluded reference simply disappears — `quant.sf` stops summing to 1e6 and to the mapped count, with nothing saying why.

`warn_mass_on_unreported_refs` turns that into a loud warning naming the offending references and asking for a report. It's the symptom-level check, so it covers both invariants without depending on either.

## Test

Pins the contract end to end on a decoy-aware index with bias on: three rows, no decoy, TPM exactly 1e6, NumReads accounting for every mapped fragment, and the guard silent on a healthy run.

Suite **317/0**, clippy clean. Independent of #1160 — different files, either order.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f5e7f0a32fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.