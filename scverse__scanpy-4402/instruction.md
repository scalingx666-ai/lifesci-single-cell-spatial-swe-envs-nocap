# Issue

**Title:** docs: clarify var_names lookup when gene_symbols is set

## Description

**LLM usage**

- [x] LLM or coding agent used: Claude Opus 5.5
- [x] If one was used, I, a human, have reviewed, understood and tested every changed line

The change corrects the `var_names` description in `src/scanpy/plotting/legacy/_docs.py`: when `gene_symbols` is set, `var_names` must contain values from `adata.var[gene_symbols]`.
When `use_raw` is in effect, the lookup uses `adata.raw.var`.

The shared text is in the docstrings for `heatmap`, `tracksplot`, `dotplot`, `matrixplot`, `stacked_violin`, and their three plot classes.
The internal `_prepare_dataframe` docstring and the description of mapping values have the same correction.
Lookup behavior stays the same.

- [x]
- [x] [Tests][] included: `test_var_names_gene_symbols_documented` checks all five public plot functions.
- [ ] [Release notes][] not necessary because:

All five new docstring cases fail without the change and pass with it.
The same three violin-image comparisons fail on the branch and at the merge-base, with identical RMS values.

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/page/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `101daba900c8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.