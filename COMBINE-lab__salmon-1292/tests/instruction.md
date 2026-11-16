# Issue

**Title:** fix(align): judge only the strand of a RAD hit under an outward library type

## Description

## Problem

`-l OU` (and the other outward types) mapped zero fragments on the default BAM path.

A RAD hit stores only the fragment's leftmost position, so the reader cannot tell whether a pair points inward or outward. `rad_frag_format` therefore always reports opposite-strand pairs as inward. Under an outward `-l`, the orientation check then rejects every pair.

Measured on 200 outward pairs under `-l OU`:

| | `num_mapped` |
|---|---|
| before | 0 |
| after | 200 |

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line. I reproduced it with the new test. Tracked in #1283.

## Fix

New `rad_compatible` in `crates/salmon-align/src/rad.rs`, used by the eq-class and bias passes. Under an outward `-l`, an opposite-strand pair is taken as outward, so only its strand is judged.

## Limits

This makes outward libraries work; it does not make the RAD path able to see orientation. Inward pairs in a run given `-l OU` now pass too, where they used to be dropped along with everything else. Telling them apart would need the orientation stored per hit, which is a format change, so I left it out.

`-l A` cannot detect an outward library on this path, and this does not change that.

## Verification

- New test `an_outward_library_maps_on_the_rad_path` in `crates/salmon-align/tests/deterministic_bam.rs`. I saw it fail without the fix (`0` versus `200`).
- `salmon-align` tests pass, and clippy on `salmon-align` is clean with `-D warnings`. The whole workspace suite was not run on this branch; CI covers it.
- This touches the same lines as #1285, so whichever merges second needs a small rebase.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de66d4933616`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.