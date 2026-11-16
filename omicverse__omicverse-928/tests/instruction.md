# Issue

**Title:** release: omicverse 2.3.1

## Description

Patch release. Every change in it is a reachability repair or a documentation correction found by checking 2.3.0's documented API against its own source while building agent tooling. **No numerical behaviour changed.**

Contents (already merged, this only bumps the version and the guide pointer):
- #927 — three real bugs plus a set of docstrings describing behaviour the code does not have
- omicverse/omicverse-tutorials#104 — tutorial 05 could not run against 2.3.0
- omicverse/omicverse-tutorials#105 — 2.3.1 release notes

The three that break working-per-the-docs code:

| | |
|---|---|
| `ov.synbio` | 33 names were in a submodule's `__all__` but missing from the lazy map, so `ov.synbio.<name>` raised `AttributeError`. A test now walks every submodule's `__all__` in both directions, and runs without the `[synbio]` extra so CI actually executes it. |
| `ov.pl` | `slopeplot(test='auto')` raised — it passed the raw string to `_run_test` instead of the shared resolver. Now resolves to Wilcoxon signed-rank, the paired counterpart, since `slopeplot` requires `subject=`. |
| `ov.space` | `niche.neighborhood` / `niche.utag` called `sc.tl.leiden(flavor='igraph')`, a scanpy 1.10 keyword, while we pin `scanpy>=1.9`. Now passed only when the installed signature accepts it. |

Two things deliberately **not** changed, with the reasoning recorded in the code:
- `predict_localization` can never return `'secreted'` — but that is correct for *E. coli*, where a Sec signal peptide delivers to the periplasm. The scoring stands; the four-compartment claim was what was wrong.
- `mmgbsa(md_refine_ns=0)` writes ~1000 frames rather than the "single scored frame" its comment claimed. Scoring one frame would report `std=0` and `sem=0` — a precision MM-GBSA does not have — so the comment was fixed instead of the number.

CI on #927 was green on 3.10 / 3.11 / 3.12 (full suite, ~30 min each). Merging this and pushing `v2.3.1` triggers the PyPI publish.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52def44434ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.