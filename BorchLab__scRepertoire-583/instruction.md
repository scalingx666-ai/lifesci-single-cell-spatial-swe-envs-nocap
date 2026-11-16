# Issue

**Title:** Fix getCirclize self-links and clonalHomeostasis group ordering (v2.9.2)

## Description

Two bug fixes reported via GitHub issues, plus a patch version bump to 2.9.2.

> `getCirclize()`: self-links always returned 0 #582 

With `include.self = TRUE` (the default), every diagonal (self) link came back as 0, regardless of how many private clones a group held.

The self-link value in symmetric mode is meant to be a group's private clone count:

```value = (all clones in group) - (clones in group also seen in another group)```

The clone table is built with `table()`, which materializes a zero-count row for every clone-by-group combination. The subtraction step that removes shared clones never filtered on `n > 0`, so every clone appeared to exist in every other group and the subtraction cancelled the entire count to 0.

Fix: require n > 0 in the subtraction so it only counts clones actually observed in other groups. Applied the same guard to the n.shared statistic in the `include.metadata = TRUE` path, which had the identical over-counting bug.

> `clonalHomeostasis()`: clonal groups ordered alphabetically #581 

The clonal groups sorted alphabetically (`Hyperexpanded, Large, Medium, Rare, Small`) instead of by proportion bin, placing `Rare` before `Small`.

The fill categories came out of reshape() as a plain character vector, which ggplot factorizes alphabetically.

Fix: cast the categories to a factor ordered by the proportion bins, so the legend and stacking follow `Hyperexpanded → Large → Medium → Small → Rare`. The ordering is derived from the `clone.size` bins, so custom bins stay correct. `combineExpression() `already ordered its `cloneSize` factor this way, so no change was needed there.


Changes
- `R/getCircilize.R` — add n > 0 guard to self-link subtraction and n.shared
- `R/clonalHomeostasis.R` — order fill categories by proportion bin
- `NEWS.md` — 2.9.2 bug-fix entries
- `DESCRIPTION` — version bump to 2.9.2

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6bb6e79f7ae7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.