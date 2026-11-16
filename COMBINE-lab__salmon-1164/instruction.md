# Issue

**Title:** fix(group 2): a flag that does nothing must say so — reads vs -a/--rad

## Description

**Group 2 of 4** (#1140). The mode×flag applicability check existed for sketch-vs-selective-alignment and for the online-only knobs, but had never been written for **reads vs `-a`/`--rad`** — ~30 mapping, scoring, seeding and orphan-policy flags accepted there in total silence, including `--sketch` itself, which names a mapping algorithm that cannot run.

Stacked on #1163 (Group 1); GitHub will show only this group's diff once that merges.

## Two were missing features, not missing warnings

| Flag | Was | Now |
|---|---|---|
| `--hardFilter` in `-a`/`--rad` | Inert — **but meaningful there**: the path really does soft-weight by `exp(-scoreExp·(best−score))`, and `--scoreExp` was already deliberately plumbed in, so the policy was half-applied | Keeps only best-scoring placements at weight 1, mirroring `score.rs` |
| `--discardOrphans` in `--rad` | Worked under `-a`, inert under `--rad` — so requantifying a RAD contradicted the `-a` run that wrote it | Honoured |

Both apply in the bias posterior pass as well as the eq-class pass, so the bias model is trained over the same placements as the weights it explains.

Pinned by result, not by message. On a contested fixture (200 ambiguous fragments, txA scoring one point better, plus unique anchors for both so neither is zeroed): soft weighting shares the mass **253.1 / 66.9**; `--hardFilter` gives all 200 contested fragments to txA, **260.0 / 60.0**.

## Everything else warns by name

Through **one shared helper** rather than another round of hand-rolled blocks — which also retires the `--writeRad shape an intermediate RAD` grammar bug in the two batch-E blocks now routed through it:

- reads-mode mapping knobs in `-a` and `--rad`
- alignment-only knobs (`--errorModel`/`--noErrorModel`/`--numErrorBins`/`--discardOrphans`) in reads mode
- pair-only knobs under single-end `-r`
- RAD-shaping knobs on reads `--online` (which `-a --online` and `--rad` already warned about)
- bias sub-knobs without any of `--seqBias`/`--gcBias`/`--posBias`
- ten selective-alignment knobs missing from the `--sketch` list

Detecting "the user passed this" requires the value to be optional, so **14 more valued flags are Option-typed** with defaults applied at use, continuing the established pattern. `--decoder` also gains a `value_parser`, so a typo is rejected in every mode rather than only where the flag is consumed.

## One finding I did not apply

An assessor read the stale help text and concluded `--noSingleFragProb` is online-only and should join the online-only inert list. **It is not.** The D14 work implemented it on the deterministic and RAD paths, and it demonstrably flips the answer there — txA 60 / txB 0 versus txA 0 / txB 60 on a contested-orphan fixture. Adding that warning would have introduced a new false claim. The stale help text is Group 4's problem, and is on its list.

Suite **328/0**, clippy clean. Group 5 remains tracked in #1162.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d86550fa159`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.