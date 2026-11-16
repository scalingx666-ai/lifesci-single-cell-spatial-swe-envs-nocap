# Issue

**Title:** fix: strand-judge --recoverOrphans pairs in one-pass mode

## Description

Closes audit finding F16 from the #1140 behavior review (the last confirmed instance of the #1136 pattern).

## The bug

The `--recoverOrphans` rescue site built its `RawMapping` with `format: None`, and the one-pass strand filter accepts a `None` format unconditionally ("accept rather than guess"). Under a stranded `-l`, recovered wrong-strand pairs therefore bypassed the compatibility filter entirely and were counted as compatible mappings. The deterministic path never had this hole — the RAD stores both mates' strand bits and `quantify_rad` judges recovered pairs like any other pair — so this was also a silent one-pass-vs-deterministic divergence.

## The fix

A recovered pair's orientation is genuinely *observed*, not guessed: the anchor's strand is real mapping evidence, and the rescued mate is opposite by construction (the rescue searches inward geometry). So the site now fills `format` via `observed_paired_format(anchor.is_fw, !anchor.is_fw)`, and one-pass judges recovered pairs exactly as deterministic always has. One-line semantic change.

## The test

`recovered_pairs_are_strand_judged` builds a fixture where rescue is *necessary*: mate 2 gets a substitution every 10 bases, so no clean 31-mer survives for seeding (unmappable alone) while banded DP still clears the score floor. It pins three things:

- rescue actually engages — orphan count drops versus a `recover_orphans: false` run of the same reads (guards against the fixture silently mapping normally);
- the matching library type (`ISF`) keeps ≥90% of recovered pairs — no over-filtering;
- the opposite type (`ISR`) now drops them (≤10% mapped) **and counts them incompatible** — this assertion fails on `develop`.

`cargo fmt` clean, clippy clean, full workspace suite 308/0.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9e2bdbe401eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.