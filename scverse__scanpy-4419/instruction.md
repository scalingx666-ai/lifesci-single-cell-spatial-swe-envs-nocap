# Issue

**Title:** fix: keep infinite normalized dispersions in `n_top_genes` cutoff

## Description

**LLM usage**

- [x] LLM or coding agent used: Claude Opus 5.5 via oh-my-pi
- [x] If one was used, I, a human, have reviewed, understood and tested every changed line
- [x] 
- [x] [Tests][] included or not required because:
- [ ] [Release notes][] not necessary because:

`_subset_genes` maps NaN to `-inf` with `np.nan_to_num`, which also turns `+inf` into the largest finite float. When at least `n_top_genes` genes have `+inf` normalized dispersion, `_nth_highest` returns `+inf` as the cutoff, no gene passes `>= cutoff`, and nothing is selected. Passing `posinf=np.inf` keeps them infinite.

The `+inf` values come from `flavor="cell_ranger"`: undetected genes get dispersion 0, and when they are more than half of the lowest mean bin, that bin's median and MAD are both 0. This also happens on real data. With pbmc3k filtered as in the tutorial and cut to the first 500 cells, `n_top_genes=10` selects 0 genes on `main` and the 390 tied `+inf` genes with this change (the same for any value up to 390). All genes tied at the cutoff are flagged, as they already are for finite values. Whether a zero MAD should give `+inf` in the first place is a separate question that I left alone.

The new test fails on `main` and passes here. The full test suite shows no new failures.

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/page/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3daa1fcf18f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.