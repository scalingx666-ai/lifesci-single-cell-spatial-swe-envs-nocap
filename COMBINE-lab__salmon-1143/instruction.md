# Issue

**Title:** Run-spanning `total_time_seconds` and `inference_path` in `meta_info.json`

## Description

First of the maintainer-side items from #1140 (issues 3 and the `inference_path` suggestion from @BenjaminDEMAILLE's review).

- **`total_time_seconds` spans the whole run.** `AlignQuantOptions` gains `prior_seconds` / `external_start_time`; the three two-phase drivers (reads `--deterministic`, `-a --deterministic`, genome projection) capture phase-1 wall time and start stamp and hand them to `quantify_rad`. Previously the file reported only the requant (Ben measured 0.447s against 18.2s wall — 40× off).
- **`inference_path` in `meta_info.json`**: `"deterministic"` (RAD input, incl. `--deterministic` phase 2), `"online"` (one-pass reads / streaming BAM), `"none"` (mapping-only `--skipQuant` pass whose file a phase 2 would rewrite). Makes the default flip auditable from existing output.

Tests pin both: `quantify_rad` with `prior_seconds = 100` reports ≥100 s with the external start stamp and `"deterministic"`; the reads e2e asserts `"online"`.

.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c498cbf07244`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.