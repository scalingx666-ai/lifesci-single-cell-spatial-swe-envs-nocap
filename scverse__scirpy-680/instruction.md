# Issue

**Title:** Filter unused categories from clonotype network legend

## Description

## Summary
- The clonotype network plot legend now only shows categories that are actually present in the plotted data
- Previously, all categories from the full dataset were listed, making it hard to identify colors when only a subset of categories appeared in the network
- Collects which category colors are used in the pie chart rendering, then filters the legend entries accordingly

## Test plan
- [ ] Verify legend only shows categories present in the plotted network subset
- [ ] Legend still works correctly when all categories are present
- [ ] No visual regression for non-categorical coloring (continuous variables, uniform color)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db9006b201d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.