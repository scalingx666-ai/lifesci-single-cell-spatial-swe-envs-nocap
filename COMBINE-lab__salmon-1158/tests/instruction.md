# Issue

**Title:** audit batches C and D: the flags that only worked on the deprecated path

## Description

Stacked on #1157. These are the two batches offered to @BenjaminDEMAILLE on #1140; nothing came in and they gate nothing else, so rather than hold 2.6.0 we implemented them — Ben, if you have anything local, say so and we'll drop ours.

Every finding here has the same shape: a flag that is accepted, documented, and does nothing on the 2.6.0 default path while working under `--online`.

## Batch C — the default `-a` path

- **C10 `--discardOrphans`** was read only by `quantify_alignments`. The deterministic writer now drops half-mapped fragments before they reach the RAD, by the same rule the online path applies (a placement backed by fewer than two records), inside `analyze_group` so the FLD and naive-eq tallies see exactly the placements that get written. Guarded on a paired library, as the online path guards it — with single-end reads every placement is an "orphan" and the flag would discard the entire run.
- **C11 `--scoreExp`** was never forwarded to deterministic `-a`, though phase 2 applies a score exponent to AS-scored placements exactly as it does to selective-alignment ones. The comment claiming alignment mode "has no such term" was true only of the online path.
- **C12 the `-l A` caveat** — that detection can only sample what the aligner chose to report — fired only on the online path, so the default alignment path detected a library type and said nothing. Hoisted into one helper called by all three producers: the caveat is a property of the input, not of the estimator reading it.

## Batch D — inference knobs

- **D13 `--perNucleotidePrior`** was ignored in two distinct places, on *every* path: Gibbs hardcoded `per_transcript_prior: true` at all three call sites, and bootstrap replicates passed `eff_lens: None` into the replicate EM, which silently falls back to the flat prior. Both now follow the flag.
- **D14 `--noSingleFragProb`** stopped at the mapping pass, so it was inert on every RAD path including the default. The RAD quantifier's orphan weighting honours it now, taking salmon's flat `log(0.375e-10)` penalty instead of the bounded-CMF ambiguous weight.
  **Worth flagging for review:** the obvious constant to reach for, `salmon_core::math::LOG_EPSILON`, is `-1e10` — a log-zero sentinel, not salmon's orphan penalty. Using it would annihilate the placement rather than disfavour it. The correct value (`-23.998…`, matching `processor::LOG_EPSILON` on the reads path) is defined locally with a comment saying exactly this, because the wrong one is one autocomplete away.
- **D15 `--meta`** promises uniform initialization in its own log line, and online `-a` is the one path where that is a real choice — its optimizer warm-starts from the online estimates unless told otherwise. Every other path starts uniform by construction, which is why the claim was true everywhere else.

**Not fixed, by standing decision:** `--noSingleFragProb` on the deprecated online *alignment* path, which already weights every orphan flat by construction — that is the F17 divergence documented in #1157.

## Tests

`--discardOrphans` takes a fixture from 65 mapped fragments to 40 and strips the orphan-only transcript's mass on the deterministic path.

The `--noSingleFragProb` fixture took some care, and the shape is worth knowing for future tests on this path: the RAD carries **one map type per fragment**, so a fragment cannot be a proper pair on one transcript and an orphan on another — a mixed fragment reads back as a proper pair on both. And an orphan's modelled weight only differs between transcripts when the length it bounds falls inside the FLD's support. So the fixture trains the FLD with proper pairs on a third transcript, then contests the orphans between a long transcript and the 3' end of a short one, where only ~150 bases remain and a ~300-base fragment cannot fit. Modelled, the mass goes to the long transcript; flat, both placements tie and effective length hands it to the shorter one. The flag flipping the answer completely is the point — it was silently doing nothing.

Full workspace suite **316 passed / 0 failed**, clippy clean.

This closes the last of the 111 confirmed audit findings.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `78b7a9177f8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.