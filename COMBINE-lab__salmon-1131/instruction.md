# Issue

**Title:** feat(quant): report strand-incompatible fragments in lib_format_counts.json

## Description

.

## Problem

On a stranded library, fragments whose every mapping lands on the wrong strand are discarded (default `--incompatPrior 0`), but the count never reached the output. `lib_format_counts.json` hardcoded `compatible_fragment_ratio: 1.0` and `num_compatible_fragments = num_mapped`, so the only way to get the wrong-strand fraction was a second strandedness pass over an alignment (RSeQC `infer_experiment` on a STAR BAM in the reporter's case).

That number is a free contamination estimator. Double-stranded input (genomic DNA carry-over from incomplete DNase digestion) maps to either strand with equal probability, so an excess of incompatible fragments implies a comparable amount of contamination sitting *on* the expected strand, indistinguishable from RNA once assigned. Comparing the ratio across a cohort flags the affected libraries at quantification time.

## Change

Two per-worker counters in the mapping pass (merged into the shared atomics at thread end, like the existing orphan/decoy tallies, so the hot path touches no shared memory), written to `lib_format_counts.json`:

| field | meaning |
|---|---|
| `num_incompatible_fragments` **(new)** | fragments that mapped but had no strand-compatible placement |
| `num_compatible_fragments` | fragments with at least one strand-compatible placement, now measured instead of aliased to `num_mapped` |
| `compatible_fragment_ratio` | the two counts' ratio, instead of a hardcoded `1.0` |

Notes:

* `num_incompatible_fragments` is counted under any `--incompatPrior`. Under the default 0 the fragment is dropped and is therefore not in `num_assigned_fragments`; above 0 it is kept at reduced weight and is.
* `num_compatible_fragments` was wrong with `--incompatPrior > 0`: such fragments count as mapped without being compatible. With the default prior the value is unchanged from before.
* Every other field keeps its C++ name and meaning, so the file stays a drop-in for existing readers. The new key is additive.
* The `--deterministic` mapping pass writes this file and then hands off to a RAD requant that does not rewrite it, so it tallies the same way (from the expected format an explicit `-l` already fixes). Under `-l A` neither path counts the fragments consumed before the library type is inferred, so the two counts can sum to less than the mapped total.

Not addressed here: `strand_mapping_bias` is still `0.0`, and there is no modelling of the residual same-strand contamination (question 2 of the issue). Both are separate pieces of work; this PR is the "zero extra compute" number the issue asks for.

## Testing

`cargo test --workspace` green; `cargo clippy --workspace --all-targets` and `cargo fmt --check` clean.

Two new end-to-end tests in `crates/salmon-quant/tests/quant_end_to_end.rs`, on simulated inward-FR reads:

* `stranded_lib_format_counts_report_incompatible_fragments`: under `ISF` every fragment is compatible (ratio 1.0, count 0); under the opposite `ISR` the new count is the whole library and the ratio collapses to ~0, while `num_assigned_fragments` stays at the (near-zero) mapped total.
* `deterministic_mapping_pass_reports_incompatible_fragments`: the `--deterministic` phase-1 pass reports the same, which would otherwise silently be zero for every deterministic run.

Docs: field semantics and the contamination rationale added to `website/src/content/docs/reference/output-formats.md`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d53f40c98ec8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.