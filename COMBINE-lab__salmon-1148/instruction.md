# Issue

**Title:** feat(align): --noLengthCorrection and --noFragLengthDist in the RAD path (#1140 PR B)

## Description

PR B of #1140, the feature work. Neither knob existed in the RAD quantifier, so both were accepted and dropped under `--deterministic`: the run corrected effective lengths and weighted by fragment length whatever the user asked for. `--noLengthCorrection` is the one with a constituency, since 3' tagged-end protocols do not sample a transcript's interior uniformly and the corrected length describes something the data never did.

## Mirroring reads mode, not reinventing it

| knob | reads mode | this PR |
|---|---|---|
| `--noLengthCorrection` | effective length is the raw `ref_len`; bias correction disabled (`bias_on && !no_length_correction`) | same, in `quantify_rad`'s eff-length block and its `bias_on` gate |
| `--noFragLengthDist` | `frag_log_prob` returns `LOG_1`, suppressing both the proper-pair PMF term and the orphan/single-end ambiguous term | same, in the eq-class pass and in the bias pass's posterior, the two places reads mode applies it |

Per your warning not to guess on the orphan term: `processor::frag_log_prob` returns early before either branch, so the ambiguous term goes too. I mirrored that rather than only zeroing the proper-pair PMF.

Both flags are wired for `--deterministic`, `-a` and `--rad`, since all three run the same quantifier and none of them had them.

## Measured

3000-transcript fixture, 300k pairs, `quant.sf` rows where `EffectiveLength == Length`:

```
det                                   0 / 2996
det --noLengthCorrection           2996 / 2996      (one-pass --noLengthCorrection: 2996 / 2996)
det --noLengthCorrection --gcBias  2996 / 2996      byte-identical to the line above
det --noFragLengthDist                0 / 2996      lengths untouched, estimates changed
```

The `--gcBias` line is the gate working: bias is disabled rather than silently correcting lengths the run was told not to correct.

## Testing

Two tests in `crates/salmon-align/tests/rad_input.rs`, both at the RAD level so they pin the semantics rather than the CLI wiring:

- `no_length_correction_uses_raw_lengths`: the default shortens every transcript; with the flag, `eff_lengths == lengths` exactly.
- `no_frag_length_dist_changes_weights_not_lengths`: two transcripts of equal length (so the divisor cannot explain anything), each fragment ambiguous between them with placements reporting fragment lengths of 190 (the FLD mean) and 700 (its far tail). With the term, the near-mean placement takes the mass (>290 of 300); without it, the two are indistinguishable and it splits evenly (within 1). Effective lengths identical in both runs.

Worth recording that the obvious fixture does not work: with two long transcripts the proper-pair term is `pmf(flen) - cmf(txpLen)` and `cmf` is 0 for anything much longer than the fragment distribution, so the term cancels between placements and the flag has no visible effect. Making the transcripts short instead makes the effective-length divisor dominate and the EM goes winner-take-all. Equal lengths plus differing per-placement fragment lengths is what isolates the term.

## Left out

The online `-a` path (`quantify_alignments`) still supports neither, which C++ salmon does. Kept out to hold this to the RAD path the default flip needs, as you offered; happy to follow up if you want the parity before 2.6.0.

## Overlap

Touches `run_deterministic` (two forwarded fields) and the `-a` / `--rad` option blocks in `main.rs`, so it overlaps #1146 and my #1144 / #1147 by a few lines each. Trivial rebase whichever order they land in.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5eed9672aa4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.