# Issue

**Title:** bank: dclp-unidentified-literary-papyri, six pitfalls from one negative run

## Description

## Bank correction: six pitfalls for `dclp-unidentified-literary-papyri`

One standard run on this target (2026-10-16, 3 h, open corpora only: idp.data DCLP at f0fcec2, First1KGreek 03776b3, canonical-greekLit 0189b9c, canonical-latinLit 128a05a) found no candidate identification, but it measured five things about the criterion and one about its sources that the entry should warn about. This PR appends them to the entry's `pitfalls`. No other field is changed; `SHA256SUMS` and the generated `known-unknowns/` page are left for the maintainers.

### 1. The literal pool is 6 records

Reading clause (a) as written (every work-level author/title element unidentified), 6 transcribed records qualify. The "about 80 Opus incertum" records mostly carry a named author (Menander, Archilochus, Philodemus, Demetrius Laco, "Paulus?"), which fails (a). A further 656 transcribed records have no work-level element at all; by title about half are magical, medical, liturgical or school texts. The entry should say whether "unknown work of a named author" and "no work-level element" are in scope.

### 2. Clause (c)'s junction requirement excludes most fragments by construction

"12 consecutive legible letters spanning at least 2 papyrus lines" needs both lines preserved at the junction. 651 of the 1,028 transcribed identified records whose author is in the open corpora (63%) lose both line ends and cannot form such a run whatever they contain. Calibration example: BKT 9 120 (Homer, 423 legible letters) scores zero under the clause and 22 letters at the Iliad without it.

### 3. Twelve letters is chance-level

Against 170 M Greek letters, 254 of 662 records reach a 12-letter two-line window with one mismatch; order-2 Markov controls with the same line lengths reach 16-17. What discriminates is the distinct-works count of clause (e) and a within-line or Markov null. The survivors of those are quotations (Psalms, Homer, Poimandres), recipe parallels with Galen already cited in the records' re-editions (P.Berl.Möller 13, P.Oxy. 80 5244), liturgical formulae and philosophical commonplaces.

### 4. Clause (d)'s line-order null ties its own hits

A line-order shuffle re-creates the real two-line junction about once in n-1 controls, so a one-junction hit ties the null and cannot reach p < 1e-4 under it: 13 of 13 shortlisted parallels tied or lost on 2026-10-16 while beating all 400 within-line-shuffle and Markov controls. The entry should name a null that does not contain the real junction and a level reachable by simulation (400 controls floor at 1/401).

### 5. Supplied letters manufacture hits

Counting `<supplied>` letters as legible, 110 of 662 records reached the threshold only through restored text (29 with windows of 20 or more). The strip must keep supplied, unclear, expanded and counted-gap positions as wildcards rather than deleting them, and treat gaps of unknown extent as hard breaks.

### 6. The clause (f) live pages are behind challenge pages

papyri.info serves an Anubis proof-of-work page to a plain client; trismegistos.org answered plain GETs with connection failures and a 403 challenge. An honest verifier can read the idp.data XML (the same data) but not the HTML or LDAB pages; the verification method should say so.

### What was not found

No record survived (a), (c), (d), (e) and (f) together; nothing is claimed. Reports, the frozen pre-registration, code (stdlib and numpy; a 6-gram index over the three corpora builds in two minutes) and outputs are in the contributor's workspace and can be shared on request.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab114dcb1aad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.