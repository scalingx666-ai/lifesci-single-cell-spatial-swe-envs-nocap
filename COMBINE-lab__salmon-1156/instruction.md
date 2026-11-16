# Issue

**Title:** audit batch E: the mode×flag applicability sweep

## Description

Stacked on #1155 (GitHub will retarget to `develop` when it merges). The ~20 accepted-but-inert flag×mode combinations from the #1140 audit, resolved under one rule: **a flag that does nothing must say so** — and where the fix was as cheap as the warning, it acts instead.

## Now acting (real fixes)

- **`--dumpBiasModels` works on every RAD/alignment path.** It silently vanished with the 2.6.0 flip: only the one-pass reads writer had a dump site, gated off by phase 1's `skip_quant`. The dump now lives in the shared output writer, fed by each pass's own `BiasDump` (which `quantify_rad` and `quantify_alignments` already build); forwarded via `requant_options` (field test extended), the `-a` branch, and the `--rad` block.
- **`--rad` forwards `--numGCBins`/`--conditionalGCBins`/`--biasSpeedSamp`/`--noBiasLengthThreshold`** — the same omission class `requant_options` was built to end, recurring in the `--rad` block while `--gcBias` itself was wired.
- **`--genome`/`--juncMissDiscount` without `--annotation` are clap errors** (`requires`), not silently dead flags.
- **Genome-projection `--skipQuant` applies the deliverable rule (#1149):** the projected RAD is the run's only output, so it lands in the output directory under its stable name and is kept — previously a "successful" run deleted it and left the output directory empty.
- **`-g` under `--skipQuant` no longer writes a zero-filled `quant.genes.sf`** (while announcing success) on the alignment/RAD/online paths; it logs why it skipped, matching the deterministic reads driver. All six drivers now behave identically.

## Now saying so (warn-by-name)

- **Sketch mode names every selective-alignment knob it ignores**: `--ma/--mp/--go/--ge`, `--minScoreFraction`, `--fullLengthAlignment`, `--orphanChainSubThresh`, `--discardOrphansQuasi`, `--orphansRequireUnmappedMate`, `--sparseSeeds`/`--refMEMs`/`--uniMEMs`. The valued knobs are Option-typed (defaults applied at wiring) so "explicitly passed" is detectable — the #1150 pattern. `--sketchStrictOrphans` without `--sketch` warns in reverse.
- **`--online` in `--rad` mode tells the truth**: it says a RAD is always quantified offline instead of promising the one-pass path, and it no longer suppresses the online-knob inertness warning — `--rad X --online -f 0.9` used to drop `-f` silently behind a misleading deprecation notice.
- **RAD-shaping flags** (`--writeRad`/`--keepRad`/`--radScratchDir`/`--radCompress`/`--noCompressRad`) warn on the two paths that write no RAD (online `-a`, `--rad` input); `--radCompress` is Option-typed for it.
- **`--writeUnmappedNames`** warns in `-a` and `--rad` modes — only the reads mapper tracks per-read mapping failures.

## Verified stale (no change needed)

`--dumpEq`/`--dumpEqWeights` in `-a`/`--rad` and the `--skipQuant --dumpEq` warning were already fixed by the #1147 follow-ons; the audit entries predate them.

## Tests

`flag_matrix.rs` drives one index through every row end-to-end: `bias_models.txt` exists on the default path (fails on develop), sketch warns by name with two non-warning controls, `--rad --online` surfaces both truths and the un-suppressed knob warning, clap rejects orphaned `--genome`, and `--skipQuant -g` skips with its reason and no gene file. Full workspace suite 318/0, clippy clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a51a9890026`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.