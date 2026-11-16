# Issue

**Title:** fix(map): apply the strand-compatibility filter in sketch mode

## Description

.

## Problem

Sketch-mode `ScoredMapping`s carried `format: None`, which `is_compatible` deliberately accepts for a proper pair rather than guessing. Two consequences:

1. **No strand filtering in sketch mode**: on a stranded library, every wrong-strand proper pair was kept at full weight (neither dropped under the default `--incompatPrior 0` nor down-weighted above it). Only orphans were judged (status-based).
2. **`-l A` blind in sketch mode**: the library-type detector samples only placements with `format.is_some()`, so it never received a sample and always fell back to `IU` with zero evidence.

The orientation was available the whole time — the RAD writer and the deterministic FLD already derive the observed format from the very same fields (`is_fw` / `mate_is_fw`).

## Fix

Fill `format` at the two sketch construction sites, mirroring selective alignment:

- proper pairs: `observed_paired_format(h.is_fw, h.mate_is_fw)`
- single-end reads: the SA-style `SingleEnd` observed format (filtering is status-based for SE either way; this feeds `-l A` detection)
- orphans: stay `None`, as in SA — judged by status + strand, not sampled for detection

No hot-path cost: the field was already constructed per mapping; this changes what is stored, not how much work is done.

## Verification

200k real unstranded pairs (poly-A human RNA-seq), sketch mode:

| run | num_mapped before | after | selective alignment |
|---|---|---|---|
| `-l ISF` | 168,036 (~99% — nothing filtered) | **86,546 (~51%)** | 86,134 |
| `-l ISR` | 167,991 (~99%) | **87,373 (~51%)** | 86,889 |
| `-l A` | fell back to `IU`, zero samples | **detects `IU` from 50k samples** | detects `IU` |

New regression test (`pseudoalignment_strand_filter_respects_library_type`) on simulated inward-FR reads: under `ISF` everything maps with mass conserved; under `ISR` (essentially) nothing may map (was ~100% before the fix); `-l A` resolves `ISF` from the detector's samples instead of falling back to `IU`.

Full workspace suite 279 passed / 0 failed; fmt clean; clippy clean apart from two pre-existing `chunks_exact` lints in untouched files that only the newest clippy flags.

Note for #1131: with this fix, sketch mode's `lib_format_counts.json` counters become meaningful for proper pairs too; the sketch caveat added to the docs there should be trimmed once both are in (happy to do that in whichever lands second).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c7f95c66005`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.