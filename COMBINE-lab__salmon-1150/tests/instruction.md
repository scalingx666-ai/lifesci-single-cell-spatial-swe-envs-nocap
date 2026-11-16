# Issue

**Title:** 2.6.0: deterministic quantification is the default; `--online` is the deprecated escape hatch

## Description

The flip proposed, measured, reviewed, and prepared in #1140. A bare `salmon quant` now takes the deterministic two-phase path in **every input mode** — selective alignment, sketch, and `-a` — producing byte-identical `quant.sf` at any thread count. The evidence (both our 10M-pair real-data measurements and @BenjaminDEMAILLE's independent replication on a hostile high-multimapping fixture) is summarized in the issue and in the drafted release notes.

## What this PR does

- **Default dispatch flip** in reads mode and alignment mode; genome projection (inherently RAD-based) warns that `--online` has no meaning there.
- **`--online`** selects the pre-2.6 one-pass path for one deprecation cycle (removal planned for 2.7.0), announcing its deprecation when used. `--online --deterministic` is a clap-level conflict error. (No `--onePass` alias — nothing exists to be compatible with, and `--online` is the better name.)
- **`--deterministic` stays accepted as a no-op** — it's in scripts and CI configs already.
- **No silent inertness**: the online-only knobs (`--forgettingFactor`, `--numAuxModelSamples`, `--numPreAuxModelSamples`) are now `Option`-typed so "explicitly passed" is detectable, and warn *by name* when passed without `--online`. `--noLengthCorrection`/`--noFragLengthDist` warn under `--online -a` (the one path that never supported them) instead of doing nothing.
- **Progress spinner for the deterministic mapping pass**, handed into the driver so it stops at the phase-1/phase-2 boundary instead of spinning frozen through the requant.
- **`bam_score_tags_unusable` reaches `meta_info.json`'s `diagnostics`**: new `AlignQuantOptions::extra_diagnostics` handoff carries the phase-1 AS verdict (from #1145) into the phase-2-written metadata, so pipelines that only keep the output directory see it.
- **Docs** (CLI reference + RAD/determinism guide) reframed around the new default; **`docs/release-notes-2.6.0.md`** drafted, covering the flip, the deprecation schedule, the behavior deltas (`--skipQuant` semantics, `-l A` accounting, AS-scored `-a`), the disk story, and the full accounting/correctness cycle behind it.

## Tests

A binary-level e2e pins the contract: bare run → `inference_path: deterministic` with the intermediate cleaned up; `--online` → `online` + deprecation announcement; `--deterministic` accepted; `--online --deterministic` errors; an inert knob warns by name under the default and draws no inertness complaint under `--online`. Full workspace suite: **303 passed / 0 failed**; clippy/fmt clean.

## Sequencing

Lands **after** #1148 and #1147 (expected trivial conflicts in the `run_quant` wiring blocks; I'll rebase as they merge). Remaining from #1140 after this: the two pre-flip validation runs called for on the issue — the 26M-pair full evaluation set and a slow-disk machine — which should gate the actual 2.6.0 tag rather than this merge.

.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `697e44ee8122`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.