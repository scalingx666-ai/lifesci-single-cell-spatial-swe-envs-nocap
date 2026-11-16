# Issue

**Title:** kit: propagated_bar.py, the bar a deletion already reaches (26 scu cells are beaten with no search)

## Description

## What

`kit/propagated_bar.py` (standard library, Python 3.9+) and `kit/tests/test_propagated_bar.py` (8 tests). For a two-column record table (N, value) it computes the propagated bar B(N) and lists the **free cells**: rows that a construction with no search already beats.

- Equal balls (radius, larger is better): deleting balls from the posted packing of a larger N' keeps its radius, so B(N) = max over listed N' >= N of r(N').
- Sum of radii (csqv, `--direction up`): arbitrarily small circles can always be added to the packing of a smaller N', so B(N) = max over listed N' <= N of S(N').

Values are compared exactly, as fractions of the decimal strings.

```sh
python3 kit/propagated_bar.py https://packomania.com/scu/txt/radius.txt --margin 1e-11 --n 733
# rows 1134 (N 1..1024192); free cells at margin 1e-11: 26
# N = 733: row 0.058531064607; bar 0.058943675866 from N' = 734; FREE (the row is beaten by the bar)
```

## Why: the live tables on 2026-10-20

Counts with each target's own margin (protocol sha256 `3c99aa5d...5332`, frozen 00:40Z before the run; files fetched 00:41Z):

| table (bank target) | margin | rows | free cells | N range | largest gap | inside a queued range |
|---|---|---|---|---|---|---|
| csq | 1e-10 | 3147 | 1813 | 501 to 9984 | 8.35e-4 (N = 992, from 1003) | all 1813 |
| csc, crt, ccq (csq p2) | 1e-10 | 250, 299, 600 | 0 | | | |
| cci | 1e-11 | 2735 | 193 | 652 to 3943 | 5.81e-5 (N = 1260, from 1261) | all 193 |
| chx (cci p3) | 1e-10 | 355 | 1 | 266 | 6.85e-7 (from 267) | no |
| scu | 1e-11 | 1134 | 26 | 209 to 807 | 4.13e-4 (N = 733, from 734) | none (no scu entry) |
| ssp (scu p2) | 1e-10 | 1153 | 25 | 917 to 100000 | 7.86e-4 (N = 30000, from 30093) | all 25 |
| hsp4, hsp5, hsp6 | 1e-10 | 299, 299, 258 | 0 | | | |
| csqv (up) | 1e-11 | 583 | 0 | | | |

The success criteria compare a claim with the row for the same N only. At a free cell, deleting balls from the posted N' file meets the numeric part of the criterion with no search. We checked three cells exactly (integer arithmetic on the decimal strings, our own checker, not this script):

- scu N = 733 from `scu734.txt` (Last-Modified 17 Oct 2026 16:58 GMT), last centre deleted: r* = 0.0589436758646, row 0.058531064607, +4.13e-4. scu has no queued range and no 2026 History entry for N = 733, so this deletion would pass the whole current scu criterion.
- csq N = 992 from `csq1003.txt`, last 11 centres deleted: r* = 0.0167080057180, row 0.015873015873, +8.35e-4 (inside a queued csq range).
- cci N = 1260 from `cci1261.txt`, last centre deleted: r* = 0.0263286272671, row 0.0262705607204, +5.81e-5 (inside the queued cci range).

The posted N' files reproduce their own rows to 1.4e-12, 1.4e-14 and 3e-31.

An observation, not a claim about intent: the csq and cci free cells match, in count and range, the 15-Oct-2026 Vidit Patankar entries on `pending-requests.html` (1813 csq candidates in 501-9984; 193 cci candidates in 652-3943). The ssp range matches too (17 candidates for 25 free cells). So the queue rule covers those cells today; scu and chx have no such cover.

Open claims checked against B(N): none is a pure deletion. #526 (scu 733) and #527 (scu 739) beat B(N) by 7.7e-8 and 5.1e-7; most of their margin over the row (4.1e-4 and 9.6e-5) is the free cell. The accepted packomania packages on main (12 hsp4, 3 scu rows) are not at free cells.

## Left for you

- Criterion wording: compare a claim with B(N) instead of the row for N (same margins), and report the margin over B(N) in TROPHY_CASE. The bank already does this for kissing numbers: `kissing-number-dims-25-48` compares with "B(d) = the maximum, over every dimension d' <= d (a configuration in R^{d'} embeds in R^d)". The facts are added as bank pitfalls in #377 (scu, ssp) and #390 (csq, cci, chx); the criteria themselves are untouched.
- Whether the script belongs in `kit/` or `bank/`; it is standalone and imports nothing from `check_run.py`.

## Checks

- kit tests 92/92 (84 + 8 new) on Python 3.11.17 and 3.9.6 at main `a900a108`.
- The new tests include negative controls: a monotone table has no free cell, one planted inversion gives exactly one, ties and the margin boundary, exact comparison beyond float precision, the up direction.
- Merged with all our open PRs (the bank commits that point here: #372 `03b0e56d`, #377 `123fbbed`, #390 `bbafd088`) on main `a900a108`: no conflicts, 163 tests OK (skipped=1) on Python 3.11.17 and 3.9.6.

### Code tables: checked, nothing to fix (exploratory)

The same question for the code tables in the bank: King's DNA tables (`dnacodes.html`, sha256 `25d6e9f8...`, GC and GC,RC, 170 cells each) under monotonicity in d (and, for GC, appending one symbol), and Brouwer's `Andw.html` (Last-Modified 19 Oct 2026 08:39 GMT, 1305 cells, d = 4..18) under A(n,d,w) >= A(n-1,d,w), A(n-1,d,w-1), the averaging shortenings ceil(A(n+1,d,w)(n+1-w)/(n+1)) and ceil(A(n+1,d,w+1)(w+1)/(n+1)), and A(n,d+2,w). No cell is beaten by a neighbour in either site (planted inversions are all found; Brouwer applies shortening and lengthening himself). Not checked: propagation from the improved cells of arXiv:2608.13906 and arXiv:2607.19550, which the constant-weight criterion also compares with.

### Note 2026-10-21

The bar this tool computes counts table rows only. Release v1.1 of github.com/vidigoat/optimization-records (2026-10-18T05:54:31Z) already holds packings above both the row and this bar for 25 of the 26 scu free cells (details in #377, commit 87f1677). So a free cell is a cell where the table is weak, not a cell where a deletion-based claim is novel; a novelty check still has to read the public releases.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69e90f785b77`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.