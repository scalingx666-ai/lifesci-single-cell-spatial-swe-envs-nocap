# Issue

**Title:** [bank] ebl-unidentified-fragment-overlaps: three pitfalls from two negative runs (restorations in the signs field, uncurated genres, unreachable null level)

## Description

## Bank correction: three pitfalls for `ebl-unidentified-fragment-overlaps` (and one cross-reference in `ebl-fragment-identification`)

Two runs on this target (2026-10-15 and 2026-10-16, standard effort, public eBL API only) found no candidate indirect join, but they found three things about the data and the criterion that the entry should warn about. This PR adds them to the entry's `pitfalls` and adds a one-line `pitfalls` cross-reference to the sibling target. No other field is changed; `SHA256SUMS` and the generated `known-unknowns/` page are left for the maintainers.

### 1. The public `signs` field includes editorial restorations

`fragments/all-signs` and each record's `signs` string encode bracketed (restored) text exactly like attested signs. A shared run between two fragments can therefore be an editor's restoration matched against itself, or against the parallel it was restored from.

Evidence: the strongest raw-sign overlap of the 2026-10-15 run, VAT.18937 | VAT.25937 (71 consecutive shared signs, 0 other fragments containing the run), was refuted by a three-skeptic panel: 42 of the 71 signs on VAT.18937 are restorations, and both tablets are barley-income receipts of one archive (Pedersén 2025, nos. 91 and 108). Re-aligning all 1,109 raw-sign overlaps on attested positions only (derived from the records' text tokens, `enclosureType` without `BROKEN_AWAY`) kept 123 hits; every Babylon cluster vanished.

### 2. "Genre absent" mostly means uncurated, and the labels live elsewhere

The unidentified set defined by the bulk genre queries (8,780 transliterated fragments with no genre or only OTHER:Uncertain) is dominated by administrative and legal records. Their identification sits in `references[].notes` (e.g. "Income of barley") and in `dossiers` (e.g. "Babylon N1"), which a clause (a) check on `notes`/`genres`/`joins` never reads. Of 808 records of candidate pairs, only 37 were clean once those fields and archive-edition references were included.

### 3. Clause (d)'s level is not reachable by simulation

With thousands of candidate pairs, p < 1e-4 after Bonferroni is below 1e-8, while a pooled line-shuffled null of 10^4 to 10^5 samples floors at about 1e-4. "Beats every control" remains checkable; the entry should state a reachable level or allow a pre-registered parametric tail.

### What was not found

No pair of unidentified fragments survived all clauses on attested signs. The seven that survived the strict record check were Old Assyrian loan contracts and Ur III accounts sharing formulae with amounts and names, not compositions. Status NOTHING; nothing is claimed here.

Full reports, pre-registrations (three versions, each frozen before its search), code and panel files are in the contributor's workspace and can be shared on request.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab114dcb1aad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.