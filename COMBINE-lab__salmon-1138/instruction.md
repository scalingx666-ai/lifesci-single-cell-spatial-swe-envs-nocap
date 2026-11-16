# Issue

**Title:** Measure library-format counts (C++ semantics) and support `-l A` in every quantification path

## Description

## Context

An audit of the post-#1131/#1137 state — do all paths (selective alignment, sketch, alignment-based, each with and without `--deterministic`/RAD requant) properly record and report the compatible/incompatible tallies and the library-format counts, and properly infer + filter under `-l A`? — found the compat/incompat side complete, but three drifts from C++ in the rest of `lib_format_counts.json`, and one `-l A` hole.

### What had drifted

Comparing against C++ `ReadExperiment::summarizeLibraryTypeCounts`:

- **`num_frags_with_concordant_consistent_mappings` / `num_frags_with_inconsistent_or_orphan_mappings`** were proxied by the paired-vs-orphan split. In C++ they derive from the per-observed-format histogram: fragments whose *observed format agrees* with the expected one (exactly the expected format for a stranded type; either strandedness of the expected orientation for an unstranded one) versus everything else.
- **`strand_mapping_bias`** was hardcoded `0.0`. C++ measures the sense share of the expected orientation's two variants — the number behind the classic "potential strand bias > 1% in an unstranded protocol" warning, which was also missing.
- **The raw per-format counts** (`IU`, `ISF`, `ISR`, …, `SR`) that C++ appends to the JSON were absent.

And the one `-l A` gap: **online alignment mode (`-a`) skipped `-l A` entirely** — no detection, no filtering, no tally, `expected_format: "a"` verbatim. (C++ never detected strandedness there either, falling back to `IU`/`U` by pairedness — but our deterministic `-a` path already detects via its RAD pass, so the online path was internally inconsistent.)

## What this PR does

- **Every path now tallies the observed-format histogram** — one count per distinct format among a mapped fragment's placements, from the raw placements *before* any filtering (per-worker arrays merged at thread end; zero shared-state traffic on the hot path): one-pass SA + sketch, the deterministic mapping pass, the RAD requant (hence `--deterministic` phase 2, `--rad`, `-a --deterministic`, and genome-projected quant), and the online BAM pass.
- **One shared writer.** The file is now a single struct (`salmon_core::LibFormatCountsFile`) holding the C++ derivation and all three C++ warnings, used by both the reads-mode and align/RAD writers — the paths structurally cannot drift apart again.
- **`-l A` in online `-a`**: the same prefix-sampling `LibraryTypeDetector` reads mode uses, fed from the BAM/SAM stream (read type via peeking the first record's flags, C++'s `peekBAMIsPaired`), with the same detect → lock-in → filter-the-remainder semantics, and the detected type reported in the result and the JSON. The BAM path also gains the library-type-mismatch diagnostic under an explicit `-l`, inferred from the end-of-run histogram.

### Three pre-existing `expected_format` mislabelings, caught by the new assertions

All the same inversion — reporting the *detected* format where the *declared* one was used to filter:

1. The align/RAD writer preferred `detected_library_type` over an explicit `-l` (the RAD derive pass detects even under explicit types, for the mismatch diagnostic) — a `-l ISF` requant reported `expected_format: "IU"`.
2. `quantify_rad` computed `detected_library_type = detected.or(baked)`, while its filter resolves `baked.or(detected)` — under `-l A` with a baked header format that disagreed with re-derivation, the JSON named a format the filter never used.
3. Reads-mode `--deterministic` let `DiscreteFld`'s detection override an explicit `-l` in `QuantResult::library_type` — a deterministic `-l ISR` phase-1 file said `expected_format: "ISF"`.

## Verification

- **Tests pin exact counts by construction in every path**: RAD requant (explicit types; `-l A` detect-then-filter on a skewed mix; baked-header-format-is-authoritative), BAM/SAM (explicit types; paired and single-end `-l A` detection incl. the pairedness peek), and reads-mode e2e (SA, sketch, deterministic phase 1) — plus exhaustive unit tests of the C++ derivation in `salmon-core`.
- **Real data** (200k-pair unstranded subset, GENCODE v49): all paths report the identical histogram (`ISF` 79220 / `ISR` 79992), `strand_mapping_bias` 0.4976 (correctly ≈0.5 for an unstranded library), and under `-l ISR` the measured ratio ~0.51 with concordant = the `ISR` count. `-l A` resolves `IU` identically in SA, sketch, and `--deterministic` runs.
- **Accounting only**: `--deterministic -l ISR` `quant.sf` is **byte-identical** to the pre-change build. (The one behavioral addition is `-a -l A`, which previously did nothing.)
- Full workspace suite: **288 passed / 0 failed**; clippy and fmt clean.

## Note for release notes

`docs/release-notes-2.5.1.md` states "quantification results are unchanged", which #1137 (sketch strand filter) already supersedes and this PR adds to (`-a -l A` now detects). The next release's notes should cover #1136/#1137/#1131 and this PR together — likely as 2.6.0 rather than 2.5.1; left out of this PR since the version call isn't mine to bake in.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f440ba706daa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.